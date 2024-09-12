---
layout: default
title: WhatsAuth in WordPress
parent: Web Installation
grand_parent: Guides
---

# Guide to Using WhatsAuth Form Validator in WordPress

## Introduction

This guide will help you integrate the WhatsAuth Form Validator into a WordPress website to validate phone numbers via WhatsApp. It ensures that phone numbers entered in your forms are verified before submission.

## Steps to Integrate WhatsAuth Form Validator in WordPress

### 1. **Install a Form Plugin (if needed)**

If you don’t have a form plugin installed, you can use plugins like **Contact Form 7**, **WPForms**, or **Gravity Forms** to create a contact form.

For this guide, we’ll assume you are using a form plugin where you can add a phone number input field.

### 2. **Set an ID for the Phone Number Field**

Once your form is created, you need to assign an **ID** to the phone number input field.

#### For Contact Form 7:
1. Go to your form in **Contact Form 7**.
2. Find the phone input tag and assign an ID:
   
   Example of phone field in Contact Form 7:
   ```html
   [tel* phone id:phone_field]
   ```
   This assigns the ID `phone_field` to the phone number input field.

#### For WPForms or Gravity Forms:
1. In the **Form Builder**, click on the phone input field.
2. In the **Advanced Settings** for the field, assign an ID such as `phone_field`.

   Example:
   - **ID:** `phone_field`

### 3. **Add WhatsAuth Script to the WordPress `<head>`**

1. Log in to your WordPress **Admin Dashboard**.
2. Go to **Appearance > Theme File Editor** (or use a child theme if preferred).
3. In the **Theme Files** section, open the `header.php` file.
4. Before the closing `</head>` tag, add the following code to include the WhatsAuth script:

```html
<script src="https://static.whatsauth.com/plugins/whatsauth-form/latest/validator.js"></script>
```

This loads the WhatsAuth Form Validator script on all pages.

### 4. **Add Initialization Script to WordPress Footer**

1. In **Theme File Editor**, open the `footer.php` file.
2. Before the closing `</body>` tag, add the following initialization script:

```html
<script>
  window.$WhatsAuthForm.init({
    inputSelector: "#phone_field",  // The phone input field to validate
    apiKey: "YOUR_API_KEY",  // Replace with your WhatsAuth API key
    description: "Please verify your phone number using WhatsApp.",
    placeholder: "Click to validate your phone number",
    primaryColor: "#2ecc71",
    secondaryColor: "#27ae60",
    btnText: "Verify via WhatsApp"
  });
</script>
```

- Replace `"YOUR_API_KEY"` with your actual WhatsAuth API key.
- Ensure that the `inputSelector` matches the ID of the phone number field you set in your form.

Alternatively, if you prefer not to edit theme files directly, you can add this script to the footer using a plugin like **Insert Headers and Footers**:
1. Install and activate **Insert Headers and Footers** plugin.
2. Go to **Settings > Insert Headers and Footers**.
3. In the **Scripts in Footer** section, add the initialization script above.

### 5. **Publish or Update Your WordPress Site**

After adding the code to the `<head>` and `<body>` sections, save the changes and **publish or update** your WordPress site. The phone number input in your form will now require WhatsApp validation before submission.

## Additional Notes

- **Customizing Styles**: You can customize the styles of your phone input field directly within your form plugin's settings, or add custom CSS to your theme's stylesheet or use the **Additional CSS** section in the Customizer.
  
- **Selector Flexibility**: The `inputSelector` can target any phone number input field. If you are using a different ID or class for the phone field, ensure the correct selector is used.

By following these steps, you will successfully integrate the WhatsAuth Form Validator into your WordPress form and provide secure WhatsApp-based phone number validation.


## Reference

For more detailed information on adding custom code to your WordPress theme, please refer to the official WordPress documentation:

[WordPress: Adding Custom Scripts to Your Site](https://wordpress.com/go/website-building/how-to-properly-add-javascript-to-wordpress-3-top-methods/)

This guide provides comprehensive instructions on how to properly add JavaScript and custom code to your WordPress site, which is essential for implementing the WhatsAuth Form Validator and customizing your site's functionality.

