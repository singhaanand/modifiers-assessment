// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract DrivingLicense {
  // Mapping to store the age of each user
  mapping(address => uint) public age;

  // Mapping to store whether a user owns a vehicle
  mapping(address => bool) public ownsVehicle;

  // Modifier to check if the caller has set their age
  modifier ageIsSet() {
    require(age[msg.sender] > 0, "Age is not set. Please set your age first.");
    _;
  }

  // Modifier to check if the user is eligible based on age (18 or older)
  modifier isEligibleAge() {
    require(age[msg.sender] >= 18, "You are not old enough for a driving license.");
    _;
  }

  // Function to set the age of a user
  function setAge(uint _age) public {
    // Using require to ensure the age is a reasonable value
    require(_age > 0 && _age < 150, "Invalid age provided.");

    // Setting the age for the sender's address
    age[msg.sender] = _age;
  }

  // Function to set vehicle ownership status of a user
  function setVehicleOwnership(bool _ownsVehicle) public {
    // Setting the vehicle ownership status for the sender's address
    ownsVehicle[msg.sender] = _ownsVehicle;
  }

  // Function to check eligibility for a driving license with modifiers
  function checkEligibility() public view ageIsSet isEligibleAge returns (bool) {
    // Modifier checks have already happened, no additional checks needed here
    return ownsVehicle;
  }
}
