
# 🌐 FrontAccounting Migration Tutorial (Beginner Friendly)

### 🚀 Goal
This tutorial will help **beginners** and **junior team members** easily move a **FrontAccounting (FA)** system from one hosting account to another.  
Follow each step carefully — no advanced technical skills are required.

---

## 🧾 What You’ll Need
Before starting, make sure you have:

- ✅ Access to **old hosting** (current FA installation)
- ✅ Access to **new hosting**
- ✅ cPanel or File Manager on both
- ✅ Basic login credentials for the MySQL database

---

## 🧱 Step 1 — Backup the Old FrontAccounting Installation

### 🗂 1.1 Backup Files
1. Log in to **your old hosting cPanel**.
2. Open **File Manager**.
3. Navigate to your FA installation folder (usually `public_html` or `public_html/fa`).
4. Select all files and folders:
5. Click **Compress** → choose **ZIP**.
6. Download the ZIP file to your computer.

---

### 🗃 1.2 Backup Database
1. In **cPanel**, open **phpMyAdmin**.
2. Find your FA database (you can check the name inside `/config_db.php`).
3. Click the database name.
4. Go to **Export** → choose:
- Export method: **Quick**
- Format: **SQL**
5. Click **Go** to download the `.sql` file.

📦 You now have two backups:
- FA files (`.zip`)
- Database (`.sql`)

---

## 🏗️ Step 2 — Create a New Database on the New Hosting

1. Log in to your **new hosting cPanel**.
2. Go to **MySQL® Databases "Manage My Databases"**.
3. Under **Create New Database**, type a name same as old one (e.g. `myfa_db`).
4. Under **Add New User**, create:
```

Username: myfa_user
Password: (choose a strong password)

```
5. Click **Create User**.
6. Under **Add User to Database**, select the new user and database.
7. Click **Add** → select **ALL PRIVILEGES** → save.

📝 Note these details:
```

Database name: myfa_db
Database user: myfa_user
Database password: ********
Host: localhost

```

---

## 🧹 Step 3 — Clean or Prepare Database
If you already have a partial database (from a failed import):
1. Open **phpMyAdmin** → select your new database.
2. Scroll down → click **Check All** → choose **Drop**.
3. Confirm deletion (this clears old tables).

---

## 💾 Step 4 — Adjust SQL File (if needed)

If your **old hosting used MySQL 8** and your **new hosting uses MariaDB 10.x**,  
you’ll need to fix the collation issue.

### 🧩 How to Fix:
1. Open the `.sql` file in **Notepad++** or **VS Code**.
2. Press `Ctrl + H` to **Find and Replace**.
3. Replace all:
```

utf8mb4_0900_ai_ci

```
with:
```

utf8mb4_general_ci

```
4. Save the file.

💡 This makes your database compatible with most servers.

---

## 📤 Step 5 — Import the Database to the New Hosting

1. In **new cPanel**, open **phpMyAdmin**.
2. Select the new empty database.
3. Click **Import**.
4. Choose your `.sql` file.
5. Click **Go**.
6. Wait for “✅ Import successfully finished.”

---

## 📂 Step 6 — Upload FrontAccounting Files to the New Hosting

1. Open **File Manager** on the **new hosting**.
2. Go to `/public_html/` (or create a folder like `/public_html/fa/`).
3. Upload your `.zip` file (the one you downloaded earlier).
4. Select it → click **Extract**.
5. Ensure all folders appear properly.

🧾 Folder structure should look like:
```

/public_html/index.php
/public_html/config_db.php
/public_html/company/
/public_html/includes/
/public_html/modules/

````

---

## ⚙️ Step 7 — Update the Configuration File

Edit `/config_db.php` to use your **new database details**.

Example:
```php
<?php
$db_connections = array (
  0 => array (
    'name' => 'Your Company',
    'host' => 'localhost',
    'dbname' => 'myfa_db',
    'dbuser' => 'myfa_user',
    'dbpassword' => 'YourPassword',
    'tbpref' => '0_',
    'collation' => 'utf8mb4_general_ci',
  ),
);
?>
````

💡 Save the file when done.

---

## 🔒 Step 8 — Fix File Permissions

Make sure the following folders are writable by your web server:

| Folder      | Permission |
| ----------- | ---------- |
| `/company/` | 755 or 775 |
| `/backup/`  | 755 or 775 |
| `/tmp/`     | 755 or 775 |

You can set this in **File Manager → Change Permissions**.

---

## 🚀 Step 9 — Test Your Website

1. Visit your new FA site URL:

   ```
   https://yourdomain.com/
   ```

   or

   ```
   https://yourdomain.com/fa/
   ```
2. You should see the **FrontAccounting login** screen.
3. Log in with your old credentials.
4. Check:

   * Company name appears correctly.
   * Dashboard and menus load.
   * Reports and transactions open normally.

---

## 🧩 Step 10 — Final Cleanup

* ✅ Delete the `.zip` backup from the server (for security).
* ✅ Keep a local backup copy of `.zip` and `.sql`.
* ✅ Document your database credentials and migration date.

---

## 🧠 Quick Tips

| Tip                                 | Description                                            |
| ----------------------------------- | ------------------------------------------------------ |
| 💾 Always back up before migration  | Files + Database                                       |
| ⚙️ Use phpMyAdmin for import/export | Easier for beginners                                   |
| 🧹 Fix collation issues             | Replace `utf8mb4_0900_ai_ci` with `utf8mb4_general_ci` |
| 🛡 Keep permissions correct         | Avoid login or upload errors                           |
| 🔍 Verify after migration           | Check dashboard, users, reports                        |

---

## ✅ Migration Checklist

| Step                           | Done |
| ------------------------------ | ---- |
| Exported database              | ☐    |
| Downloaded FA files            | ☐    |
| Created new database           | ☐    |
| Imported `.sql` successfully   | ☐    |
| Uploaded and extracted files   | ☐    |
| Updated `config_db.php`        | ☐    |
| Fixed folder permissions       | ☐    |
| Tested and verified            | ☐    |
| Deleted backup zip from server | ☐    |

---

### ✨ You’re Done!

Your FrontAccounting is now fully migrated to the new hosting 🎉
All company data, invoices, and transactions are safe and working as before.

---

**Written by:**
🧩 **Slash WTech Team**
[https://slash.wtechhub.com](https://slash.wtechhub.com)

```

---

Would you like me to make a **PDF version** of this beginner-friendly tutorial (with screenshots and visual arrows showing each cPanel step)? It’s perfect for team onboarding and internal documentation.
```
