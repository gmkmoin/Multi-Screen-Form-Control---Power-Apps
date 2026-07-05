# Multi-Screen Form Control – Power Apps

## 📌 Project Overview

The **Multi-Screen Form Control** is a Microsoft Power Apps Canvas application that simplifies large business forms by dividing them across multiple screens. Instead of displaying all fields on a single long, scrollable form, the application uses a wizard-style navigation experience with **Next** and **Previous** buttons, allowing users to complete one section at a time.

Each screen represents a logical section of the overall form while all screens work with the same record. User-entered data is preserved as users navigate between screens, providing a seamless data entry experience.

This project was recreated from scratch based on the multi-screen form approach demonstrated by Reza Dorrani using Microsoft Power Platform.

---

## 🎯 Project Objectives

- Eliminate long scrolling forms
- Organize information into logical sections across multiple screens
- Improve readability and user experience
- Preserve entered data while navigating between screens
- Guide users through the form completion process
- Validate required information before proceeding
- Submit the entire record using a single operation

---

## ✨ Key Features

### 🖥️ Multi-Screen Navigation

- Wizard-style navigation using **Next** and **Previous** buttons
- Logical separation of form sections across multiple screens
- Simple and intuitive navigation flow
- Users complete one section at a time

### 📝 Single Record Management

Although the form is distributed across several screens:

- All screens work with the same record
- Information entered on one screen is available throughout the application
- Data remains synchronized across all screens

### 💾 Record Context Management

The application uses global variables to maintain form state.

- `varFormData` stores the selected or current record
- `varFormMode` controls Create, Edit, and View modes
- User-entered data is preserved while navigating between screens

### ✅ Dynamic Validation

- Uses the **Valid** property of forms
- Prevents users from moving to the next screen until required fields are completed
- Improves data accuracy and completeness

### 💾 Single Record Submission

Instead of submitting data from each screen individually:

- Users complete all form sections
- Validation occurs before submission
- The entire record is saved using a single `Patch()` operation
- Reduces unnecessary data source updates and improves performance

### 🔄 Form Modes

The application supports multiple operating modes:

- Create
- Edit
- View

The interface automatically adapts based on the selected mode.

For example:

- Submit button is visible in Create and Edit modes
- Read-only interface in View mode

### 🎨 User Experience Improvements

- Reduced scrolling
- Better organization of information
- Easy screen-to-screen navigation
- Improved readability
- Professional form layout
- Simplified data entry process

---

## 🖥️ Application Workflow

```text
Home Screen
      │
      ▼
Screen 1
(Basic Information)
      │
   Next
      ▼
Screen 2
(Details)
      │
   Next
      ▼
Screen 3
(Additional Information)
      │
 Validation
      ▼
Submit
(Patch)
      │
      ▼
Record Saved
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| Microsoft Power Apps (Canvas App) | User Interface |
| Power Fx | Business Logic |
| SharePoint List / Microsoft List | Backend Data Source |
| Global Variables | State Management |
| Forms | Data Entry |
| Patch() | Record Submission |
| Navigate() | Screen Navigation |
| Collections | Temporary Data Storage (Optional) |

---

## ⚙️ Power Apps Concepts Demonstrated

- Multi-screen forms
- Screen-to-screen navigation
- Global variables
- Form validation
- Record management
- Create, Edit, and View modes
- Patch()
- Navigate()
- Conditional visibility
- State management
- Data binding

---

## ⚙️ Implementation Details

### Variables

| Variable | Purpose |
|----------|---------|
| `varFormData` | Stores the selected or current record |
| `varFormMode` | Controls Create, Edit, and View modes |

### Navigation

The application uses Power Apps navigation functions:

- `Navigate()`
- `Back()`
- Next button
- Previous button

### Validation

Each screen validates the current form before allowing users to continue.

```powerfx
If(
    Form1.Valid,
    Navigate(Screen2),
    Notify(
        "Please complete all required fields.",
        NotificationType.Error
    )
)
```

### Record Submission

The entire record is submitted once using the `Patch()` function.

```powerfx
Patch(
    EmployeeList,
    varFormData,
    {
        EmployeeName: txtName.Text,
        Department: ddlDepartment.Selected.Value,
        Email: txtEmail.Text
    }
)
```

---

## 📂 Project Structure

```text
App
│
├── Home Screen
│
├── Screen 1
│     ├── Basic Information
│     └── Next Button
│
├── Screen 2
│     ├── Details
│     ├── Previous Button
│     └── Next Button
│
├── Screen 3
│     ├── Additional Information
│     ├── Previous Button
│     └── Submit Button
│
└── Data Source
```

---

## 🔄 How the Application Works

### 1. User Opens the Application

The app initializes variables and loads the first screen.

### 2. User Enters Information

Each screen contains a different section of the overall form.

Examples include:

- Basic Information
- Contact Details
- Department Information
- Additional Details

### 3. User Navigates Between Screens

Users can move through the form using:

- Next
- Previous

Previously entered information is retained throughout the navigation process.

### 4. Validation

Before moving to the next screen or submitting the form:

- Required fields are validated
- Users receive error messages if mandatory information is missing

### 5. Final Submission

After all sections are completed:

- Validation is performed
- A single `Patch()` operation saves the complete record
- The data is stored in the connected data source

---

## 🚀 Benefits

- Eliminates long scrolling forms
- Improves readability
- Better organization of information
- Enhanced user experience
- Preserves entered data across screens
- Reduces incomplete submissions
- Improves application performance
- Modular and maintainable design
- Easily scalable for enterprise applications

---

## 💡 Challenges Solved

- Long and difficult-to-navigate forms
- Excessive scrolling
- Poor organization of information
- Incomplete submissions
- State management across multiple screens
- Efficient record updates using a single submission

---

## 📚 Learning Outcomes

This project demonstrates how to:

- Build large forms using multiple screens
- Design user-friendly navigation flows
- Manage application state using variables
- Preserve user input across screens
- Implement form validation
- Use `Patch()` for efficient data updates
- Build reusable Create, Edit, and View screens
- Improve usability through structured form navigation

---

## 🛠️ Potential Use Cases

This architecture can be adapted for many enterprise applications, including:

- Employee Onboarding
- Customer Registration
- Leave Applications
- Expense Claims
- Purchase Requests
- Asset Requests
- Vendor Registration
- Inspection Forms
- Audit Checklists
- Survey Applications
- Service Request Forms

---

## 🔮 Potential Enhancements

Future improvements could include:

- Progress indicator
- Auto-save draft functionality
- Section completion indicators
- Attachment uploads
- Role-based access control
- Conditional screen visibility
- Responsive layouts for tablets and mobile devices
- Power Automate approval workflows
- Microsoft Dataverse integration
- Review and summary screen before submission
```
