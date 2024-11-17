---
layout: default
title: Hide Access Tab On User Detail View
---
# Customizing SuiteCRM to Hide the Access Tab in User Detail View

**Introduction**
SuiteCRM is a versatile and powerful open-source CRM platform, allowing for extensive customization to meet specific business requirements. In this post, I'll share how I customized the User Detail View page to hide the Access tab, ensuring that users cannot see modules they are not allowed to access. This customization enhances the user interface by removing unnecessary or restricted information.

**Why Hide the Access Tab?**
The Access tab in SuiteCRM's User Detail View displays information about the modules a user has permissions to access. While this is useful for administrators, it may not be relevant—or even desirable—for regular users. By hiding this tab, you can create a cleaner, more user-focused interface and avoid exposing unnecessary information.

**The Code**
Below is the PHP code I used to achieve this customization. This code overrides the default User Detail View and sets the SHOW_ROLES parameter to false, effectively hiding the Access tab.

```php
<?php
if (!defined('sugarEntry') || !sugarEntry) {
    die('Not A Valid Entry Point');
}
require_once('modules/Users/views/view.detail.php');

class CustomUsersViewDetail extends UsersViewDetail
{
    public function __construct()
    {
        parent::__construct();
    }

    public function preDisplay()
    {
        parent::preDisplay();
        $show_roles = false;
        $this->ss->assign('SHOW_ROLES', $show_roles);
    }
}
```
* **How It Works**

    * File Placement:
    The code is placed in a custom directory to override the default behavior of the User Detail View. SuiteCRM automatically checks the custom directory for overridden classes, making this a straightforward process.

    * Inheritance and Extension:
    The CustomUsersViewDetail class extends the default UsersViewDetail class. This ensures that all existing functionalities of the parent class are preserved, except for the modifications we explicitly introduce.

    * Pre-display Modification:
    The preDisplay() method is overridden to set the $show_roles variable to false. This variable controls whether the Access tab is displayed. Assigning it to the SHOW_ROLES parameter ensures that the tab is hidden when the page is rendered.

* **Steps to Implement**

    * Navigate to your SuiteCRM installation's custom folder.
    * Create the necessary subdirectories to match the file path:
    custom/modules/Users/views/
    * Save the code snippet as view.detail.php in the views folder.
    * Perform a Quick Repair and Rebuild from the Admin Panel to apply the changes.
 
* **Benefits of This Customization**

    * Improved User Interface: Regular users see only relevant information, reducing potential confusion.
    * Enhanced Security: Restricting access to sensitive configuration details minimizes the risk of exposing unintended data.
    * Effortless Maintenance: The customization is cleanly implemented, making it easy to update or remove as needed.
 
**Conclusion**
This small customization showcases the power of SuiteCRM's extensibility. By leveraging its custom directory and class overriding mechanisms, you can tailor the CRM to fit your specific needs. If you have any questions or would like to share your own SuiteCRM customizations, feel free to leave a comment below.

Happy customizing! 😊
