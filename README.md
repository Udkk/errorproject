# GradingSystem Smart Contract

## Overview

The `GradingSystem` smart contract is a decentralized application designed to manage and track grades in a blockchain-based system. It allows an admin to manage teachers, while teachers can submit and update grades for students. This contract ensures that grades are managed securely and transparently.

## License

This contract is licensed under the MIT License.

## Contract Details

### Solidity Version

This contract is written in Solidity version 0.8.26.

### Features

- **Admin Functions:**
  - Add or remove teachers.
  
- **Teacher Functions:**
  - Submit grades for students.
  - Update grades for students.

- **Public Functions:**
  - Retrieve a student's grade.

### Smart Contract  

slodity 
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.26;
contract GradingSystem {
    address public admin;
    mapping(address => bool) public teachers;
    mapping(address => uint) public grades;
    mapping(address => address[]) public studentTeachers;

    event TeacherAdded(address indexed teacher);
    event TeacherRemoved(address indexed teacher);
    event GradeSubmitted(address indexed student, uint grade);
    event GradeUpdated(address indexed student, uint grade);

    modifier onlyAdmin() {
        require(msg.sender == admin, "Only admin can perform this action");
        _;
    }

    modifier onlyTeacher() {
        require(teachers[msg.sender], "Only a registered teacher can perform this action");
        _;
    }

    constructor() {
        admin = msg.sender;
    }

    // Admin functions
    function addTeacher(address _teacher) external onlyAdmin {
        require(_teacher != address(0), "Invalid address");
        require(!teachers[_teacher], "Teacher already added");
        
        teachers[_teacher] = true;
        emit TeacherAdded(_teacher);
    }

    function removeTeacher(address _teacher) external onlyAdmin {
        require(_teacher != address(0), "Invalid address");
        require(teachers[_teacher], "Teacher not found");
        
        teachers[_teacher] = false;
        emit TeacherRemoved(_teacher);
    }

    // Teacher functions
    function submitGrade(address student, uint grade) external onlyTeacher {
        require(grade >= 0 && grade <= 100, "Grade must be between 0 and 100");
        
        // Use assert to ensure that grades for a student are not overwritten
        assert(grades[student] == 0); 
        
        grades[student] = grade;
        studentTeachers[student].push(msg.sender);

        emit GradeSubmitted(student, grade);

        // Use revert to prevent low grades if required
        if (grade < 30) {
            revert("Grade is too low, student may need additional support");
            
        }
    }

    function updateGrade(address student, uint grade) external onlyTeacher {
        require(grades[student] != 0, "No grade to update");
        require(grade >= 0 && grade <= 100, "Grade must be between 0 and 100");

        // Use assert to ensure the grade is being updated correctly
        assert(grades[student] > 0); 
        
        grades[student] = grade;
        emit GradeUpdated(student, grade);
    }

    // Public functions
    function getGrade(address student) external view returns (uint) {
        return grades[student];
    }
}
# Steps to Deploy and Interact with the Contract
### Open Remix IDE:

Go to Remix IDE.
### Create a New File:

In the Remix file explorer, create a new file named GradingSystem.sol.
### Copy and Paste the Code:

Copy the smart contract code provided above and paste it into GradingSystem.sol.
### Compile the Contract:

Go to the "Solidity Compiler" tab (on the left side).
Select version 0.8.26.
Click on "Compile GradingSystem.sol".
### Deploy the Contract:

Navigate to the "Deploy & Run Transactions" tab.
Select the "JavaScript VM" environment for local testing.
Click on "Deploy" to deploy the contract.
## Interact with the Contract:

After deployment, interact with the contract using the Remix UI.
Use the deployed contract interface to call functions such as addTeacher, submitGrade, and getGrade.
Testing and Debugging
Use the built-in Remix debugger and console logs to test and debug the contract.
You can simulate various scenarios by interacting with the contract functions directly through Remix.
### Contributing
Feel free to open issues or submit pull requests for improvements and bug fixes. Please follow standard Git workflow practices.

## Acknowledgements
Solidity documentation and Remix IDE for providing a powerful development environment for smart contracts.
## Contact
For any questions or inquiries, please reach out to udit8508@gmail.com.
