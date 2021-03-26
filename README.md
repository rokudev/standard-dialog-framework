# Standard dialog framework

As part of the Roku OS 10.0 release, Roku's standard dialog framework enables developers to use new pre-built modal pop-up dialogs and build custom ones. Dialogs are used to display information to users that require their immediate attention (for example, selecting a subscription product, entering credentials or account information, informing the user that a screen is loading, and so on). These new pre-built and custom standard keyboards are summarized as follows:

- **New pre-built message, keyboard, pin pad, and progress dialogs**. These new dialogs feature updated graphics and color palette support that enable developers to provide a consistent user experience across the dialogs in their channel (and across the Roku platform as developers can easily adopt the new design of Roku OS system dialogs). In addition, the keyboard and pin pad dialogs include voice entry support for faster customer sign-ups and sign-ins. These new dialog nodes deprecate the [legacy versions](https://developer.roku.com/docs/references/scenegraph/dialog-nodes/dialog.md). 

  

- **Developer-defined custom dialogs**. Developers can design custom dialogs that may include a combination of text, buttons, bulleted lists, keyboards, loading indicators, and other building blocks. Custom dialogs also include all the features provided by the pre-built dialogs (voice, custom layout, and graphics). This provides developers with the flexibility to build and configure dialogs to meet their channel's requirements. 

## Structure

A StandardDialog contains a background image drawn under the dialog contents. The dialog contents include a vertical column containing the following areas (from top to bottom): title area, content area, button area. Each area is optional, which means a dialog may contain one to all three areas. A dialog may only have a single title area and button area, but it may have multiple content areas. The width of the title area, button area, and the sum of the widths of the content areas are always equal. 

- **Title Area**. The title area is drawn at the top of the dialog. It always contains a primary title that consists of a single line of text that briefly describes the purpose of the dialog. The title area may also include optional icons that appear left or right justified. A dialog may only have a single title area, and the title area is optional.

  

- **Content Area**. A content area is a vertical column of content items. The Content Items may include static information, such as a block of text, a bullet list or a progress indicator, or dynamic objects such as a pin pad or a keyboard. A dialog may only have a single content area, and the content area is optional. 

  

- **Button Areas**. The button area contains a vertical-arranged set of buttons. Buttons in a dialog are typically used to confirm or cancel the dialog's operation or to advance forward/backward through a multistep process. A dialog may only have a single button area, and the button area is optional.

![Basic Dialog](https://image.roku.com/ZHZscHItMTc2/BasicDialog.jpg)

## Summary

### Pre-built dialog hierarchy and examples

The pre-built message, keyboard, pin pad, and progress dialogs inherit their basic properties from the **StandardDialog** node class, which extends the **Group** node. The following table summarizes the standard dialog nodes and their hierarchy:

| Node                        | Description                                                  | Example                                                      |
| :-------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Group                       |                                                              |                                                              |
| ++ StandardDialog           | Defines the width, height, color palette, button selected, and button focused fields that are inherited by its child nodes. |                                                              |
| ++++ StandardMessageDialog  | Displays a message to the user.                              | ![standard-message-dialog](https://image.roku.com/ZHZscHItMTc2/standard-message-dialog.jpg) |
| ++++ StandardKeyboardDialog | Enables text and voice entry of strings consisting of alphanumeric characters as well as many commonly used symbols. | ![keyboard-dialog](https://image.roku.com/ZHZscHItMTc2/keyboard-dialog.jpg) |
| ++++ StandardPinPadDialog   | Enables text and voice entry of numeric digits—typically, short numeric PIN codes. | ![pin-pad](https://image.roku.com/ZHZscHItMTc2/pin-pad-dialog.jpg) |
| ++++ StandardProgressDialog | Displays a spinning progress indicator that includes a short progress message to the user. | ![progress-dialog](https://image.roku.com/ZHZscHItMTc2/progress-dialog.jpg) |

### Custom dialog hierarchy and examples

As described in the dialog structure overview, a dialog contains three areas: title, content, and button. Each of these areas has a corresponding node for building a custom dialog: **StdDlgTitleArea**, **StdDlgContentArea**, and **StdDlgButtonArea**. Each of these nodes inherits its functionality from the **StdDlgAreaBase** node, which extends the **Group** node.


- The **StdDlgTitleArea** node does not contain any child nodes. It displays the title and/or icons at the top of the dialog. 




- The **StdDlgContentArea** node may contain a number of content items such as a block of text, a bullet list or a progress indicator, or dynamic objects such as a pin pad or a keyboard. Each of these content items has a corresponding node that inherits its basic functionality from the **StdDlgItemBase** node. For example, the text block has a **StdDlgTextItem** node, the keyboard has a **StdDlgKeyboardItem** node, and so on. 

  

- The **StdDlgButtonArea** node may contain a single **StdDlgButton** node

The following table summarizes the standard dialog nodes used to build custom dialogs and their hierarchy. For completeness, the content items and buttons that may be included in the **StdDlgContentArea** and **StdDlgButtonArea** nodes are listed; however, they do not inherit any properties from the nodes. 

| Node                   | Description                                                  |
| :--------------------- | :----------------------------------------------------------- |
| Group                  |                                                              |
| ++ StdDlgAreaBase      | Provides common functionality for the **StdDlgTitleArea**, **StdDlgContentArea** and **StdDlgButtonArea** classes. |
| ++++ StdDlgTitleArea   | Contains the title information and/or icons at the top of the dialog. |
| ++++ StdDlgContentArea | Contains the main body of the dialog, which may include zero to multiple content area items (**StdDlgItemBase** nodes), which are as follows: ${std-dlg-items-table} |
| ++++ StdDlgButtonArea  | Contains any buttons (**StdDlgButton** nodes) in the button area located at the bottom of the dialog: |

{#std-dlg-items-table}

| Node                             | Description                                                  | Example                                                      |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| StdDlgItemBase                   | Provides common functionality for all content area items.    |                                                              |
| ++ StdDlgBulletTextItem          | A bulleted list of text.                                     | ![StdDlgBulletTextItem](https://image.roku.com/ZHZscHItMTc2/StdDlgBulletTextItem-v2.jpg) |
| ++ StdDlgDeterminateProgressItem | A progress indicator that represents the percentage of the progress that has been completed. | ![std-dlg-determinate-progress-item](https://image.roku.com/ZHZscHItMTc2/std-dlg-determinate-progress-item-2.jpg) |
| ++ StdDlgGraphicItem             | An image with an optional text label.                        | ![v](https://image.roku.com/ZHZscHItMTc2/std-dlg-graphic-item.jpg) |
| ++ StdDlgKeyboardItem            | Either a keyboard or PIN pad for the text and voice entry of alphanumeric/symbol strings or numeric digits (typically, short numeric PIN codes), respectively. | ![std-dlg-keyboard-item](https://image.roku.com/ZHZscHItMTc2/std-dlg-keyboard-item.jpg) |
| ++ StdDlgProgressItem            | A spinning progress indicator for tasks that take an indeterminate amount of time. | ![std-dlg-progress-item](https://image.roku.com/ZHZscHItMTc2/std-dlg-progress-item.jpg) |
| ++ StdDlgTextItem                | A block of text.                                             | ![std-dlg-text-item](https://image.roku.com/ZHZscHItMTc2/std-dlg-text-item.jpg) |

{#std-dlg-button-table}

| Node         | Description       | Example                                                      |
| :----------- | :---------------- | :----------------------------------------------------------- |
| StdDlgButton | A button element. | ![std-dlg-button-2](https://image.roku.com/ZHZscHItMTc2/std-dlg-button-3.jpg) |