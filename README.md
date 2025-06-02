# Configure-WSL-terminal-to-proxy
To configure your **WSL terminal** to use your university's proxy, follow these steps directly within your VS Code WSL terminal:

---

### 🟢 Step 1: Set Proxy for Current Terminal Session

Execute these commands for immediate effect:

```bash
export http_proxy="http://10.50.225.222:3128"
export https_proxy="http://10.50.225.222:3128"
```

Now, your terminal uses the proxy server for the current session.

---

### 🟢 Step 2: Configure Proxy Permanently

To make this persistent (recommended), add these lines to your `.bashrc` file:

```bash
nano ~/.bashrc
```

Then paste the following lines at the bottom:

```bash
export http_proxy="http://10.50.225.222:3128"
export https_proxy="http://10.50.225.222:3128"
```

Save (`Ctrl+O`, then `Enter`, then `Ctrl+X`).

Apply immediately:

```bash
source ~/.bashrc
```

---

### 🟢 Step 3: Configure APT to use the Proxy (Important for package installations)

Edit/create the file `/etc/apt/apt.conf`:

```bash
sudo nano /etc/apt/apt.conf
```

Add the following lines:

```bash
Acquire::http::Proxy "http://10.50.225.222:3128";
Acquire::https::Proxy "http://10.50.225.222:3128";
```

Save and close (`Ctrl+O`, then `Enter`, then `Ctrl+X`).

Now, package installations (`apt`) will work correctly.

---

### 🟢 Step 4: Configure Git to use Proxy (if needed)

```bash
git config --global http.proxy http://10.50.225.222:3128
git config --global https.proxy http://10.50.225.222:3128
```

---

### 🟢 Step 5: Configure Wget and Curl (useful for downloading files)

For Wget, edit `~/.wgetrc`:

```bash
nano ~/.wgetrc
```

Paste:

```
use_proxy=yes
http_proxy=http://10.50.225.222:3128
https_proxy=http://10.50.225.222:3128
```

For Curl, add to your `.bashrc` or just use environment variables (already set above):

```bash
export http_proxy="http://10.50.225.222:3128"
export https_proxy="http://10.50.225.222:3128"
```

---

### ✅ Verify Proxy Setup:

Test connectivity:

```bash
curl https://www.google.com
```

If the command returns HTML content, your proxy setup is successful.

---

### 📌 **Note:**

* Replace `10.50.225.222:3128` with any future proxy updates.
* Restart your terminal/VS Code after these configurations to ensure they take full effect.

Your WSL environment is now properly configured to use your university's proxy!
