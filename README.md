# googleSheet-password-manager

Password manager on Google Sheets that can save passwords encrypted with a shared secret key. Encryption is done on the client side.

Let’s get started

Step 1 - Create a Google Sheet
This could be the simplest of them all. Simply start a new Google Sheet. Start a fresh blank spreadsheet at sheets.google.com. 

Step 2 - Add header row

Create the header row for the columns. The headings should be:

    Name
    URL
    Username
    Password

These columns in each row will be managed by our script. You can also make the header row bold and freeze it.

You can name the sheet as you wish.

![Screenshot 2021-07-25 at 9 15 51 AM](https://user-images.githubusercontent.com/39213247/126887072-8612da1e-15c4-48b3-9246-148501ad6e6b.png)

Step 3 - Open the script editor

Next step is to open the scipt editor where we will write the code required for our tool.

Click on Tools -> Script Editor on the menubar. This will open up the script editor in a new tab.

![scripts_home](https://user-images.githubusercontent.com/39213247/126887006-09438517-238f-4485-bcfa-0fb508147299.png)

Give the script an appropriate name. This script is linked to the sheet now. All changes saved here will be available later also.

Step 4 - Create files

I have open sourced the code required for the tool at  okramjimmysingh/googleSheet-password-manager . You can copy the script files one by one to the script editor window.

Code.gs is the main Apps script file. All functions that interact with the Google Sheets are written here. You can remove the function that is already present in the editor. Once pasted, press Ctrl+S to save.

![codejs](https://user-images.githubusercontent.com/39213247/126887181-aefe20f5-7e6d-4fb4-bd1f-6f8635786402.png)

Next, create a new file called newEntry.html by going to the File -> New -> HTML File menu. Remove the existing HTML and add code from newEntry.html. Press Ctrl+S to save.

![newEntry](https://user-images.githubusercontent.com/39213247/126887201-fc060da7-83e1-4a90-a8bf-c9e61cd358b2.png)

Similarly, create new files and copy contents from decryptPassword.html and styles.html.

We have the following files in our script editor now:

    Code.gs
    newEntry.html
    decryptPassword.html
    styles.html

Step 5 - Run the script

Open Code.gs and use the Select function dropdown on the toolbar to select the onOpen function. This function is executed everytime the the Google Sheet is opened. Click on the Run button (play icon) next to the dropdown to run the function.

![codegs](https://user-images.githubusercontent.com/39213247/126887233-c97a466e-9a68-44aa-a507-6c1ebe38aca7.png)

You will now be prompted to grant permissions for the script to access the sheet. If you get a “This app isn’t verified” screen, you can safely over-ride by clicking the “Advanced” link at the bottom as you’re the developer for the app (since you just copy pasted the code).

I’m not saying copy pasting the code is safe, I am assuming you can go through couple of lines of code and figure out if it’s doing something fishy.

Once you allow the permission request and the function is ran (you might need to click the Run button agian), a new menu item will appear on the Sheet.

![1](https://user-images.githubusercontent.com/39213247/126887361-bd421e4d-3dc7-40bd-94fa-fa999281c289.png)

Step 6 - Add a password

Let’s save a password now. Click on Password Manager -> Add new password. This will open a new dialog box with several input fields.

    Name: Name of the website that you’re adding.
    URL: Login URL for the website.
    Username
    Password
    Shared secret: This is the key used to encrypt the password, you’ll need this key to decrypt it later.
    Re-type shared secret: This is to avoid any typing errors as the input is a password field.

![3](https://user-images.githubusercontent.com/39213247/126887370-ffba7516-ad08-473f-b17e-82d59a932988.png)

Once all entries are added, click on the Save button.

If there are no errors, the password is encrypted with the secret key (shared secret) and is saved into the sheet.

    Encryption happens on the browser. Raw password is not sent to the Sheet.

The password is encrypted using SJCL and upon encrypting a string with a key, it outputs a JSON object:

{

  "iv": "YfYlmYRzJBfo0xFGUNQ8Fg==",
  
  "v": 1,
  
  "iter": 10000,
  
  "ks": 128,
  
  "ts": 64,
  
  "mode": "ccm",
  
  "adata": "",
  
  "cipher": "aes",
  
  "salt": "s0McGyx/dmQ=",
  
  "ct": "Xit1P9/DeedTmGf3WZBT4V+HNHIM3jtV0K8="
  
}

This object is base64 encoded and saved into the password column.

![4](https://user-images.githubusercontent.com/39213247/126887382-7e948cbd-deff-40b1-bebc-aa1403e93d7d.png)



    Each entry can have a different shared secret.

Because each entry can have a different shared secret, you can safely share this across your team and only those who you communicate the shared secret wil be able to decrypt the corresponding password. You can also choose to have a common shared secret for team-wide sharing.

Step 7 - Decrypt a password

To decrypt a password, bring the focus to any column in the target row and then click on Password Manager -> Decrypt password menu. This will open up the decrypt password dialog box. Enter the shared secret and click the Decrypt button.

This will reveal the decrypted password in the textbox. You can click the Copy to Clipboard button if you need to copy the password.

![5](https://user-images.githubusercontent.com/39213247/126887411-de7ee518-3117-48ba-9b18-bd8dd90d860f.png)

Feedback

The project is open source. Looking forward for your suggestions and contributions.

Buy me a coffee here https://buymeacoffee.com/softwaretech                


