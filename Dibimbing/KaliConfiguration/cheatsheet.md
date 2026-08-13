# Kali Linux Basic Daily Shell & Log Analysis Cheatsheet

> A practical reference for students and beginners learning Kali Linux, Linux command-line operations, and basic Apache2 log analysis.

## 1. Terminal and Command Basics

### Check the current environment

```bash
whoami                 # Current user
hostname               # System hostname
pwd                    # Current directory
date -Is               # ISO 8601 timestamp
uname -a               # Kernel and system information
cat /etc/os-release    # Distribution information
echo "$SHELL"          # Current shell
```

### Command structure

```text
command [options] [arguments]
```

Example:

```bash
ls -lah /var/log
```

| Part | Meaning |
|---|---|
| `ls` | Command |
| `-lah` | Options: long format, all files, human-readable sizes |
| `/var/log` | Argument/path |

### Get help

```bash
command --help
man command
apropos keyword
type command
command -v command
```

Examples:

```bash
grep --help
man grep
command -v apache2
```

Useful keyboard shortcuts:

| Shortcut | Action |
|---|---|
| `Ctrl+C` | Stop the current command |
| `Ctrl+L` | Clear the screen |
| `Ctrl+D` | Exit the shell or close standard input |
| `Ctrl+R` | Search command history |
| `Tab` | Complete a command or path |
| `↑` / `↓` | Browse command history |
| `q` | Exit `less` or `man` |

## 2. Navigation and File Management

### Navigate directories

```bash
pwd                    # Print current directory
ls                     # List files
ls -lah                # Detailed listing, including hidden files
cd /var/log            # Use an absolute path
cd ..                  # Move to the parent directory
cd .                   # Refer to the current directory
cd -                   # Return to the previous directory
cd ~                   # Go to the current user's home directory
```

Path examples:

```text
/var/log/apache2/access.log   Absolute path
./evidence/output.txt         Relative path from the current directory
~/apache-lab                   Current user's home directory
```

### Create files and directories

```bash
mkdir reports
mkdir -p "$HOME/apache-lab/evidence"
touch notes.txt
printf 'Training note\n' > notes.txt
```

### Copy, move, and remove

```bash
cp -iv notes.txt evidence/
cp -r source-dir backup-dir
mv -iv notes.txt notes-old.txt
rm -i notes-old.txt
rmdir empty-directory
```

Use caution with recursive deletion:

```bash
rm -r directory-name
```

Always inspect the path before using `rm`. Avoid running destructive commands with an unresolved variable or an unexpected wildcard.

### Inspect files

```bash
file filename
stat filename
ls -lh filename
du -sh directory-name
df -h
```

| Command | Use |
|---|---|
| `file` | Identify the file type |
| `stat` | View size, timestamps, and metadata |
| `du -sh` | Check directory size |
| `df -h` | Check filesystem capacity |

## 3. Reading, Searching, and Comparing Text

### Read text files

```bash
cat file.txt
less file.txt
head file.txt
head -n 20 file.txt
tail file.txt
tail -n 50 file.txt
tail -f file.log
```

Press `Ctrl+C` to stop `tail -f`.

### Search content with `grep`

```bash
grep 'error' application.log
grep -i 'error' application.log       # Case-insensitive
grep -n 'error' application.log       # Include line numbers
grep -v '200' access.log              # Exclude matching lines
grep -E '404|500' access.log          # Match either pattern
grep -Rni 'password' ./project        # Recursive search; use only on authorized data
```

Useful options:

| Option | Meaning |
|---|---|
| `-i` | Ignore case |
| `-n` | Show line numbers |
| `-v` | Invert the match |
| `-E` | Extended regular expressions |
| `-c` | Count matching lines |
| `-R` | Search recursively |

### Find files

```bash
find . -type f
find . -type f -name '*.log'
find /var/log -type f -mtime -1
find . -type f -size +10M
```

### Compare files

```bash
diff -u old.conf new.conf
cmp file-a file-b
```

## 4. Pipes, Redirection, and Evidence

### Pipe output into another command

```bash
ls -lah /var/log | less
ps aux | grep '[a]pache2'
ss -ltn | grep ':80'
```

The pipe `|` sends the output of one command to the next command.

### Redirect output

```bash
command > output.txt       # Create or overwrite a file
command >> output.txt      # Append to a file
command 2> errors.txt      # Save error output
command &> all-output.txt  # Save standard output and errors
```

### Show and save output with `tee`

```bash
date -Is | tee evidence/timestamp.txt
ss -ltnp | tee evidence/listening-services.txt
grep -n ' 404 ' /var/log/apache2/access.log \
  | tee evidence/apache-404-lines.txt
```

Use `tee -a` to append instead of overwrite:

```bash
command | tee -a evidence/activity.log
```

### Save a reproducible command record

```bash
{
  echo "Command: ss -ltnp"
  echo "Time: $(date -Is)"
  ss -ltnp
} | tee evidence/service-check.txt
```

For every evidence file, record:

1. Command used.
2. Timestamp.
3. Raw output.
4. Interpretation.
5. Suggested next action.

## 5. Text Processing Essentials

### Count and sort values

```bash
sort file.txt
sort file.txt | uniq
sort file.txt | uniq -c
sort file.txt | uniq -c | sort -nr
```

The common counting pattern is:

```text
sort → uniq -c → sort -nr
```

### Select columns with `cut`

```bash
cut -d ':' -f 1 /etc/passwd
cut -d ' ' -f 1 file.txt
```

`cut` works best when the delimiter and field positions are predictable.

### Process columns with `awk`

```bash
awk '{print $1}' file.txt
awk '{print $1, $7}' access.log
awk '$9 == 404 {print $0}' access.log
awk '{count[$9]++} END {for (code in count) print code, count[code]}' access.log
```

Common `awk` fields for Apache combined access logs:

| Field | Typical value |
|---|---|
| `$1` | Client IP |
| `$4` | Timestamp with `[` |
| `$6` | HTTP method with quotes |
| `$7` | Requested path |
| `$9` | HTTP status code |
| `$10` | Response size |

Field positions can differ when a custom log format is configured. Confirm the format before relying on a field number.

### Count HTTP status codes

```bash
awk '{print $9}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr
```

Example interpretation:

```text
200  Successful response
301  Redirect
400  Bad request
403  Forbidden
404  Not found
500  Server-side error
```

An HTTP status code is an observation. It is not automatically a vulnerability.

## 6. Permissions, Users, and Privilege

### Read permission strings

```text
-rwxr-x---
```

| Segment | Applies to |
|---|---|
| `rwx` | Owner |
| `r-x` | Group |
| `---` | Other users |

Permission values:

```text
r = 4    Read
w = 2    Write
x = 1    Execute
```

Examples:

```bash
ls -l script.sh
chmod u+x script.sh
chmod 640 private.txt
chown user:group file.txt
```

### Check identity and privileges

```bash
whoami
id
groups
sudo -l
```

Use `sudo` only when administrative privileges are required. Do not use root by default.

## 7. Processes, Services, and Network Checks

### Process inspection

```bash
ps aux
ps aux | grep '[a]pache2'
top
pgrep -a apache2
```

### Service management

```bash
sudo systemctl status apache2
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
sudo systemctl is-active apache2
```

If `systemctl` is unavailable in a container, use the environment's service mechanism or inspect the process directly.

### Check listening ports and connectivity

```bash
ss -ltn
ss -ltnp
ss -ltnp | grep ':80'
curl -I http://127.0.0.1
curl -sS -o /dev/null -w '%{http_code}\n' http://127.0.0.1
```

Use only local or explicitly authorized targets during training.

## 8. Installing and Verifying Applications

### APT workflow

```bash
sudo apt update
apt search apache2
apt show apache2
sudo apt install apache2
dpkg -s apache2
dpkg -L apache2
apt list --installed 2>/dev/null | grep apache2
```

Important distinction:

```text
apt update     Refreshes package indexes
apt install    Installs a package
apt upgrade    Upgrades installed packages
```

### Verify a command after installation

```bash
command -v apache2
apache2 -v
dpkg -S "$(command -v apache2)"
```

Prefer Kali/Debian packages where available. Avoid using `sudo pip install` for system-wide Python changes; use `apt`, `pipx`, or a virtual environment as appropriate.

## 9. Apache2 Class Exercise

### Install and start Apache2

```bash
sudo apt update
sudo apt install apache2
sudo systemctl enable --now apache2
```

Verify the installation:

```bash
command -v apache2
apache2 -v
sudo systemctl status apache2 --no-pager
ss -ltnp | grep ':80'
curl -I http://127.0.0.1
```

### Important Apache2 locations

| Path | Purpose |
|---|---|
| `/etc/apache2/` | Apache configuration |
| `/var/www/html/` | Default website content |
| `/var/www/latihan.local/public_html/` | Document root for the training VirtualHost |
| `/var/log/apache2/access.log` | HTTP request log |
| `/var/log/apache2/error.log` | Apache errors and warnings |
| `/var/log/apache2/latihan.local_access.log` | Access log for `latihan.local` |
| `/var/log/apache2/latihan.local_error.log` | Error log for `latihan.local` |
| `/usr/sbin/apache2` | Apache server binary |
| `/etc/hosts` | Local hostname mapping used by the lab |
| `/etc/apache2/sites-available/` | Available VirtualHost configurations |
| `/etc/apache2/sites-enabled/` | Enabled virtual hosts |
| `/etc/apache2/mods-enabled/` | Enabled modules |

### Set up a local VirtualHost: `latihan.local`

This exercise creates a local-only website. The domain does not need to be registered in DNS; `/etc/hosts` maps it to the local machine.

#### 1. Map the training domain to localhost

Add the entry only if it does not already exist:

```bash
if ! grep -Eq '(^|[[:space:]])latihan\.local([[:space:]]|$)' /etc/hosts; then
  echo '127.0.0.1 latihan.local www.latihan.local' \
    | sudo tee -a /etc/hosts
fi
```

Verify name resolution:

```bash
getent hosts latihan.local
getent hosts www.latihan.local
```

Expected result should contain `127.0.0.1`.

#### 2. Create the document root and test page

```bash
sudo mkdir -p /var/www/latihan.local/public_html

echo '<!doctype html>
<html>
  <head><title>Latihan Local</title></head>
  <body><h1>latihan.local is working</h1></body>
</html>' | sudo tee /var/www/latihan.local/public_html/index.html

sudo chown -R "$USER":www-data /var/www/latihan.local
sudo find /var/www/latihan.local -type d -exec chmod 755 {} \;
sudo find /var/www/latihan.local -type f -exec chmod 644 {} \;
```

#### 3. Create the VirtualHost configuration

```bash
sudo tee /etc/apache2/sites-available/latihan.local.conf > /dev/null <<'EOF'
<VirtualHost *:80>
    ServerName latihan.local
    ServerAlias www.latihan.local

    DocumentRoot /var/www/latihan.local/public_html

    <Directory /var/www/latihan.local/public_html>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/latihan.local_error.log
    CustomLog ${APACHE_LOG_DIR}/latihan.local_access.log combined
</VirtualHost>
EOF
```

The separate access and error logs make the exercise easier to analyze than using only the global Apache logs.

#### 4. Enable the site and reload Apache

```bash
sudo a2ensite latihan.local.conf
sudo apache2ctl configtest
sudo systemctl reload apache2
```

Expected configuration-test result:

```text
Syntax OK
```

Optionally disable the default site so that the training site is the only enabled site on port 80:

```bash
sudo a2dissite 000-default.conf
sudo apache2ctl configtest
sudo systemctl reload apache2
```

#### 5. Verify the VirtualHost

```bash
apache2ctl -S
curl -i http://latihan.local/
curl -i http://www.latihan.local/
curl -i -H 'Host: latihan.local' http://127.0.0.1/
```

The response should contain the page text `latihan.local is working` and normally return HTTP status `200`.

If hostname resolution is unavailable, the `Host` header test still verifies Apache's VirtualHost selection:

```bash
curl -i --resolve latihan.local:80:127.0.0.1 \
  http://latihan.local/
```

#### 6. Generate requests for log analysis

```bash
curl -sS http://latihan.local/ -o /dev/null
curl -sS http://latihan.local/does-not-exist -o /dev/null
curl -sS http://latihan.local/robots.txt -o /dev/null

sudo tail -n 20 /var/log/apache2/latihan.local_access.log
sudo tail -n 20 /var/log/apache2/latihan.local_error.log
```

Analyze the VirtualHost-specific logs:

```bash
sudo awk '{print $9}' /var/log/apache2/latihan.local_access.log \
  | sort | uniq -c | sort -nr \
  | tee "$LAB/evidence/latihan-status-counts.txt"

sudo awk '$9 == 404 {print $7}' \
  /var/log/apache2/latihan.local_access.log \
  | sort | uniq -c | sort -nr \
  | tee "$LAB/evidence/latihan-404-paths.txt"

sudo awk '{print $1}' /var/log/apache2/latihan.local_access.log \
  | sort | uniq -c | sort -nr \
  | tee "$LAB/evidence/latihan-client-ips.txt"
```

#### VirtualHost troubleshooting

| Symptom | Checks |
|---|---|
| `latihan.local` cannot be resolved | Check `/etc/hosts` and run `getent hosts latihan.local` |
| Apache shows the default page | Run `apache2ctl -S`, verify `ServerName`, and disable `000-default.conf` if needed |
| HTTP `403 Forbidden` | Check directory/file permissions and the `<Directory>` block |
| HTTP `404 Not Found` | Confirm `DocumentRoot` and the requested path |
| Configuration reload fails | Run `sudo apache2ctl configtest` and inspect the reported line |
| Separate logs are empty | Generate a request using `http://latihan.local/`, then check the log path |

#### Remove the training VirtualHost

When the exercise is complete, disable the site and reload Apache:

```bash
sudo a2dissite latihan.local.conf
sudo apache2ctl configtest
sudo systemctl reload apache2
```

If the default site was disabled for the exercise, re-enable it when needed:

```bash
sudo a2ensite 000-default.conf
sudo systemctl reload apache2
```

### Generate test requests

```bash
curl -I http://127.0.0.1/
curl -sS http://127.0.0.1/ -o /dev/null
curl -sS http://127.0.0.1/does-not-exist -o /dev/null
curl -sS http://127.0.0.1/server-status -o /dev/null
```

The last request may return `403` or `404`, depending on the Apache configuration. Record the actual result rather than assuming it.

### Read the logs

```bash
sudo tail -n 30 /var/log/apache2/access.log
sudo tail -n 30 /var/log/apache2/error.log
sudo less /var/log/apache2/access.log
sudo tail -f /var/log/apache2/access.log
```

### Count requests by status code

```bash
sudo awk '{print $9}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr \
  | tee "$LAB/evidence/apache-status-counts.txt"
```

### Find 4xx and 5xx responses

```bash
sudo awk '$9 ~ /^4/ {print}' /var/log/apache2/access.log \
  | tee "$LAB/evidence/apache-client-errors.txt"

sudo awk '$9 ~ /^5/ {print}' /var/log/apache2/access.log \
  | tee "$LAB/evidence/apache-server-errors.txt"
```

### Find the most requested paths

```bash
sudo awk '{print $7}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr | head -n 10 \
  | tee "$LAB/evidence/apache-top-paths.txt"
```

### Find the most frequent client IPs

```bash
sudo awk '{print $1}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr | head -n 10 \
  | tee "$LAB/evidence/apache-top-client-ips.txt"
```

### Count HTTP methods

The method normally appears in field `$6`, surrounded by quotation marks.

```bash
sudo awk '{gsub(/"/, "", $6); print $6}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr
```

### Search for selected paths or terms

```bash
sudo grep -n 'robots.txt' /var/log/apache2/access.log
sudo grep -nE 'wp-login|phpmyadmin|/admin|/login' \
  /var/log/apache2/access.log
sudo grep -niE 'error|warn|crit|failed' \
  /var/log/apache2/error.log
```

Treat matches as leads for investigation. A request for `/admin` or `/phpmyadmin` does not prove that the application exists or is vulnerable.

### Save a complete evidence snapshot

```bash
mkdir -p "$LAB/evidence"

{
  echo "Apache evidence snapshot"
  echo "Timestamp: $(date -Is)"
  echo
  echo "## Service status"
  systemctl is-active apache2 2>&1 || true
  echo
  echo "## Listening port"
  ss -ltnp 2>&1 | grep ':80' || true
  echo
  echo "## HTTP headers"
  curl -I http://127.0.0.1 2>&1 || true
  echo
  echo "## Recent access log entries"
  tail -n 20 /var/log/apache2/access.log 2>&1 || true
  echo
  echo "## Recent error log entries"
  tail -n 20 /var/log/apache2/error.log 2>&1 || true
} | tee "$LAB/evidence/apache-snapshot.txt"
```

## 110. Common Log Analysis Questions

### How many requests returned `404`?

```bash
sudo awk '$9 == 404 {count++} END {print count+0}' \
  /var/log/apache2/access.log
```

### Which paths returned `404` most often?

```bash
sudo awk '$9 == 404 {print $7}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr
```

### Which client generated the most requests?

```bash
sudo awk '{print $1}' /var/log/apache2/access.log \
  | sort | uniq -c | sort -nr | head -n 1
```

### What is the latest request?

```bash
sudo tail -n 1 /var/log/apache2/access.log
```

### Are there Apache errors?

```bash
sudo grep -niE 'error|warn|crit|failed' \
  /var/log/apache2/error.log | tail -n 20
```

### How many lines are in each log?

```bash
sudo wc -l /var/log/apache2/access.log /var/log/apache2/error.log
```

## 11. Troubleshooting Quick Reference

| Problem | Useful checks |
|---|---|
| Command not found | `command -v command`, `echo "$PATH"` |
| Permission denied | `ls -l file`, `id`, use `sudo` only if required |
| Apache will not start | `systemctl status apache2`, `journalctl -u apache2 -n 50 --no-pager` |
| Port 80 is unavailable | `ss -ltnp | grep ':80'` |
| Page returns `403` | Check file permissions and Apache directory rules |
| Page returns `404` | Check the URL and document root |
| Logs appear unchanged | Generate a request, then check `tail` again |
| `awk` fields look wrong | Confirm the configured Apache `LogFormat` |

Useful Apache configuration checks:

```bash
sudo apache2ctl configtest
sudo apache2ctl -S
sudo journalctl -u apache2 -n 50 --no-pager
```

Expected result from `apache2ctl configtest`:

```text
Syntax OK
```

## 12. Cleanup After the Lab

Save evidence before stopping the service:

```bash
date -Is | tee "$LAB/evidence/finished-at.txt"
sudo systemctl stop apache2
sudo systemctl disable apache2
```

Confirm that the service is stopped:

```bash
sudo systemctl is-active apache2
ss -ltnp | grep ':80' || true
```

## 14. Daily Command Summary

| Task | Command |
|---|---|
| Show current directory | `pwd` |
| List all files | `ls -lah` |
| Change directory | `cd path/` |
| Create a directory | `mkdir -p path/` |
| Copy a file | `cp -iv source destination` |
| Move or rename | `mv -iv source destination` |
| Read a file | `less file` |
| Follow a log | `tail -f file.log` |
| Search text | `grep -n 'pattern' file` |
| Find files | `find . -type f -name '*.log'` |
| Identify a file | `file filename` |
| Check metadata | `stat filename` |
| Count lines | `wc -l file` |
| Find a command | `command -v command` |
| Check processes | `ps aux` |
| Check ports | `ss -ltnp` |
| Check service state | `systemctl status service` |
| Save output | `command | tee evidence.txt` |
| Add a timestamp | `date -Is` |


