const form = document.getElementById("form");
const password = document.getElementById("password");
const language = document.querySelectorAll("input[name='fav_language']");
const check = document.querySelectorAll("input[class='vehicle']");
const eyeicon = document.getElementById("eyeicon");
const updateButton = document.getElementById("update");

const country = ["India", "USA", "Australia"];
const state = [
  { country: "India", state: "Gujarat" },
  { country: "India", state: "Maharastra" },
  { country: "India", state: "MP" },
  { country: "USA", state: "Florida" },
  { country: "USA", state: "New_york" },
  { country: "USA", state: "Texas" },
  { country: "Australia", state: "New_South_Wales" },
  { country: "Australia", state: "Victoria" },
  { country: "Australia", state: "Queensland" },
];
const city = [
  { state: "Gujarat", city: "Surat" },
  { state: "Gujarat", city: "Vadodra" },
  { state: "Gujarat", city: "Valsad" },
  { state: "Maharastra", city: "Mumbai" },
  { state: "Maharastra", city: "Nagpur" },
  { state: "Maharastra", city: "Pune" },
  { state: "MP", city: "Bhopal" },
  { state: "MP", city: "Ujjain" },
  { state: "MP", city: "Indore" },
  { state: "Florida", city: "Miami" },
  { state: "Florida", city: "Orlando" },
  { state: "Florida", city: "Tampa" },
  { state: "New_york", city: "New_York_city" },
  { state: "New_york", city: "Hempstead_town" },
  { state: "New_york", city: "Brookhaven" },
  { state: "Texas", city: "Houston" },
  { state: "Texas", city: "Dallas" },
  { state: "Texas", city: "Austin" },
  { state: "New_South_Wales", city: "Sydney" },
  { state: "New_South_Wales", city: "Newcastle" },
  { state: "New_South_Wales", city: "Wollongong" },
  { state: "Victoria", city: "Melbourne" },
  { state: "Victoria", city: "Geelong" },
  { state: "Victoria", city: "Ballaratgour" },
  { state: "Queensland", city: "Ipswich" },
  { state: "Queensland", city: "Cairns" },
  { state: "Queensland", city: "Toowoomba" },
];
const countryS = document.getElementById("country");
const stateS = document.getElementById("state");
const cityS = document.getElementById("city");
country.forEach((country) => {
  const option = document.createElement("option");
  option.value = country;
  option.textContent = country;
  countryS.appendChild(option);
});
function updateStates() {
  const selectedCountry = countryS.value;
  console.log(countryS.value);
  stateS.innerHTML = '<option value="">select state</option>'; // reset states
  cityS.innerHTML = '<option value="">Select City</option>'; // reset cities
  if (selectedCountry) {
    const states = state.filter((item) => item.country === selectedCountry);
    states.forEach((state) => {
      const option = document.createElement("option");
      option.value = state.state;
      option.textContent = state.state;
      stateS.appendChild(option);
      console.log(option.value);
    });
    stateS.disabled = false;
    cityS.disabled = true;
  } else {
    stateS.disabled = true;
    cityS.disabled = true;
  }
}
//  update cities
function updateCities() {
  const selectedCountry = countryS.value;
  const selectedState = stateS.value;
  cityS.innerHTML = '<option value="">Select City</option>'; // reset cities
  if (selectedCountry && selectedState) {
    const cities = city.filter((item) => item.state === selectedState);
    cities.forEach((city) => {
      const option = document.createElement("option");
      option.value = city.city;
      option.textContent = city.city;
      cityS.appendChild(option);
    });
    cityS.disabled = false;
  } else {
    cityS.disabled = true;
  }
}
eyeicon.onclick = function () {
  if (password.type == "password") {
    password.type = "text";
    eyeicon.src = "eye-open.png";
  } else {
    password.type = "password";
    eyeicon.src = "closeye.png";
  }
};
viewdata();
function validate() {
  const usernameVal = document.getElementById("username").value.trim();
  const emailVal = document.getElementById("email").value.trim();
  const birthdaytimeVal = document.getElementById("birthdaytime").value.trim();
  const phone_noVal = document.getElementById("phone_no").value.trim();
  const passwordVal = document.getElementById("password").value.trim();
  const countryS = document.getElementById("country");
  const stateS = document.getElementById("state");
  const cityS = document.getElementById("city");
  const languageVal = findselected();
  const checkVal = check_data();
  if (!usernameVal) {
    setErrorMsg(username, "Name cannot be blank");
  }
  if (!emailVal) {
    setErrorMsg(email, "Email cannot be blank");
  }
  if (!birthdaytimeVal) {
    setErrorMsg(birthdaytime, "Date   cannot be blank");
  }
  if (!phone_noVal) {
    setErrorMsg(phone_no, " enter a contact number");
  }
  if (!passwordVal) {
    setErrorMsg(password, "Password cannot be blank");
  }
  if (!languageVal) {
    setErrorMsg(language[0], "Select at least one language");
  }
  if (!checkVal) {
    setErrorMsg(check[0], "Select at least one option");
  }
  // if (!countryS) {
  //   setErrorMsg(countryS, "country cannot be blank");
  // }
  // if (!stateS) {
  //   setErrorMsg(stateS, "state cannot be blank");
  // }
  // if (!cityS) {
  //   setErrorMsg(cityS, "CITY cannot be blank");
  // }
  return !document.querySelector(".error");
}
function setErrorMsg(input, errormsgs) {
  const formControl = input.parentElement;
  const small = formControl.querySelector("small");
  formControl.className = "from-c error";
  small.innerText = errormsgs;
}
function setSuccessMsg(input) {
  const formControl = input.parentElement;
  formControl.className = "from-c success";
}
//-----------------------------------------------------------------------------------------localstorage-------------------------------------------->>>>>>>>>>
let findselected = () => {
  let selectedLanguage = "";
  language.forEach((radioButton) => {
    if (radioButton.checked) {
      selectedLanguage = radioButton.value;
    }
  });
  return selectedLanguage;
};
// let selectCountry = () => {
//   for (let i = 0; i < countries.length; i++) {}
// };
let check_data = () => {
  let vehicle1 = document.getElementById("vehicle1");
  let vehicle2 = document.getElementById("vehicle2");
  let vehicle3 = document.getElementById("vehicle3");
  let result = document.getElementById("result");
  if (vehicle1.checked && vehicle2.checked && vehicle3.checked) {
    result = vehicle1.value + "," + vehicle2.value + "," + vehicle3.value;
  } else if (vehicle1.checked && vehicle2.checked) {
    result = vehicle1.value + "," + vehicle2.value;
  } else if (vehicle2.checked && vehicle3.checked) {
    result = vehicle2.value + "," + vehicle3.value;
  } else if (vehicle1.checked && vehicle3.checked) {
    result = vehicle1.value + "," + vehicle3.value;
  } else if (vehicle1.checked) {
    result = vehicle1.value;
  } else if (vehicle3.checked) {
    result = vehicle3.value;
  } else if (vehicle2.checked) {
    result = vehicle2.value;
  }
  return result;
};
//-----------------------------------------------------adding a data------------------------------------------------//
const addDataToLocal = () => {
  let username = document.getElementById("username").value;
  let email = document.getElementById("email").value;
  let password = document.getElementById("password").value;
  let birthdaytime = document.getElementById("birthdaytime").value;
  let phone_no = document.getElementById("phone_no").value;
  let language = findselected();
  let check = check_data();
  let country = document.getElementById("country").value;
  let state = document.getElementById("state").value;
  let city = document.getElementById("city").value;
  const userData = JSON.parse(localStorage.getItem("userDetails")) ?? [];
  userData.push({
    username: username,
    email: email,
    password: password,
    birthdaytime: birthdaytime,
    phone_no: phone_no,
    check: check,
    language: language,
    country: country,
    state: state,
    city: city,
  });

  localStorage.setItem("userDetails", JSON.stringify(userData));
  document.getElementById("username").value = "";
  document.getElementById("email").value = "";
  document.getElementById("password").value = "";
  document.getElementById("birthdaytime").value = "";
  document.getElementById("phone_no").value = "";
  document.getElementById("country").value = "";
  document.getElementById("state").value = "";
  document.getElementById("city").value = "";
  document
    .querySelectorAll("input[name='fav_language']")
    .forEach(function (radioButton) {
      radioButton.checked = false;
    });
  document.querySelectorAll("input.vehicle").forEach(function (checkbox) {
    checkbox.checked = false;
  });
};

let xyz = document.querySelector("form");
const submitButton = document.getElementById("submit");
form.addEventListener("submit", (event) => {
  event.preventDefault();
  if (validate()) {
    if (submitButton.style.display == "block") {
      addDataToLocal();
    } else {
      updateLocalStorage(updateButton);
    }
  }
  viewdata();
});
//----------------------------------------------------------showdata-------------------------------------------------------->>
function viewdata() {
  const abcd = JSON.parse(localStorage.getItem("userDetails"));
  if (abcd != null) {
    let html = "";
    const userDetailsArray = Object.values(abcd);
    userDetailsArray.forEach((user, index) => {
      html += `<tr>
                  <td>${index + 1}</td>
                  <td>${user.username}</td>
                  <td>${user.email}</td>
                  <td>${user.language}</td>
                  <td>${user.check}</td>
                  <td>${user.birthdaytime}</td>
                  <td>${user.phone_no}</td>
                  <td>${user.password}</td>
                  <td>${user.country}</td>
                  <td>${user.state} </td>
                  <td> ${user.city} </td>
                  <td>
                  <button type="button"  onclick="EditData(${index})" style="padding:4px;background:green">Edit</button>&nbsp;
                  <button type="button"data-toggle="modal" data-target="#myModal" id="delete-${index}" onclick="#myModal"  style="padding:4px;background:#DC143C">Delete</button>&nbsp;   
                  </td>
              </tr>`;
    });
    document.getElementById("root").innerHTML = html;
  }
}
//----------------------------------------------------------------deletedata()--------------------------------------------------------->>>

// function modal(index) {
//   <button
//     type="button"
//     id="cnfm-${index}"
//     onclick="deleteData(${index})"
//     style="padding:4px;background:#FF1493;display:block"
//   >
//     confrm
//   </button>;
// }
function deleteData(index) {
  const abcd = JSON.parse(localStorage.getItem("userDetails"));
  abcd.splice(index, 1);
  localStorage.setItem("userDetails", JSON.stringify(abcd));
  document.getElementById("username").value = "";
  document.getElementById("email").value = "";
  document.getElementById("password").value = "";
  document.getElementById("birthdaytime").value = "";
  document.getElementById("phone_no").value = "";
  document
    .querySelectorAll("input[name='fav_language']")
    .forEach(function (radioButton) {
      radioButton.checked = false;
    });

  document.querySelectorAll("input.vehicle").forEach(function (checkbox) {
    checkbox.checked = false;
  });
  viewdata();
}
//-----------------------------------------------------------------update()------------------------------------------------------------->>>>
let updateLocalStorage = (button) => {
  let rowIndex = button.getAttribute("data-index");
  console.log(rowIndex);
  const userData = JSON.parse(localStorage.getItem("userDetails"));
  const updatedData = {
    username: document.getElementById("username").value,
    email: document.getElementById("email").value,
    birthdaytime: document.getElementById("birthdaytime").value,
    phone_no: document.getElementById("phone_no").value,
    password: document.getElementById("password").value,
    country: document.getElementById("country").value,
    state: document.getElementById("state").value,
    city: document.getElementById("city").value,
    language: findselected(),
    check: check_data(),
  };
  userData.splice(rowIndex, 1, updatedData);
  localStorage.setItem("userDetails", JSON.stringify(userData));

  setTimeout(() => {
    document.getElementById("username").value = "";
    document.getElementById("email").value = "";
    document.getElementById("password").value = "";
    document.getElementById("birthdaytime").value = "";
    document.getElementById("phone_no").value = "";
    document.getElementById("country").value = "";
    document.getElementById("state").value = "";
    document.getElementById("city").value = "";
    document
      .querySelectorAll("input[name='fav_language']")
      .forEach(function (radioButton) {
        radioButton.checked = false;
      });
    document.querySelectorAll("input.vehicle").forEach(function (checkbox) {
      checkbox.checked = false;
    });
  }, 100);
};
//-------------------------------------------------------------------------------editData---------------------------------------------------------------->>
function EditData(rid) {
  const formControls = document.querySelectorAll(".from-c");
  formControls.forEach((control) => {
    control.classList.remove("error", "success");
    const small = control.querySelector("small");
    if (small) {
      small.innerText = "";
    }
  });
  const errorMessages = document.querySelectorAll(".error");
  errorMessages.forEach((errorMessage) => {
    errorMessage.innerText = "";
  });

  document.getElementById("submit").style.display = "none";
  const updateButton = document.getElementById("update");
  updateButton.style.display = "block";
  updateButton.addEventListener("click", () => {
    updateLocalStorage(updateButton);
  });

  let id = rid;
  updateButton.setAttribute("data-index", id);
  const abcd = JSON.parse(localStorage.getItem("userDetails"));
  document.getElementById("username").value = abcd[id].username;
  document.getElementById("email").value = abcd[id].email;
  document.getElementById("birthdaytime").value = abcd[id].birthdaytime;
  document.getElementById("phone_no").value = abcd[id].phone_no;
  document.getElementById("password").value = abcd[id].password;
  document.getElementById("country").value = abcd[id].country;

  let oldc = abcd[id].country;
  console.log(oldc);
  const selectedCountry = abcd[id].country;
  console.log(countryS.value);
  stateS.innerHTML = '<option value="">select state</option>'; // reset states
  cityS.innerHTML = '<option value="">Select City</option>'; // reset cities
  const states = state.filter((item) => item.country === selectedCountry);
  states.forEach((state) => {
    const option = document.createElement("option");
    option.value = state.state;
    option.textContent = state.state;
    stateS.appendChild(option);
    console.log(option.value);
  });
  const selectedState = abcd[id].state;
  const cities = city.filter((item) => item.state === selectedState);
  cities.forEach((city) => {
    const option = document.createElement("option");
    option.value = city.city;
    option.textContent = city.city;
    cityS.appendChild(option);
  });
  document.getElementById("state").value = abcd[id].state;
  console.log(document.getElementById("state").value);
  document.getElementById("city").value = abcd[id].city;
  // console.log(document.getElementById("city").value);
  let language = (document.querySelectorAll(
    "input[name='fav_language']"
  ).value = abcd[id].language);
  document.querySelector(`input[value='${language}']`).checked = true;
  let checkValues = abcd[id].check.split(",");
  let checkboxes = document.querySelectorAll("input[class='vehicle']");
  checkboxes.forEach((checkbox) => {
    checkbox.checked = checkValues.includes(checkbox.value);
  });
  viewdata();
}
const isEmail = (email) => {
  let atSymbol = email.indexOf("@");
  if (atSymbol < 1) return false;
  let dot = email.lastIndexOf(".");
  if (dot <= atSymbol + 3) return false;
  if (dot === email.length - 1) return false;
  return true;
};
//----------------------------------------------------------------------------inputfuction----------------------------------------------------->>
function inputfunction() {
  let usernameInput = document.getElementById("username");
  let username = usernameInput.value;

  if (username.length < 4) {
    setErrorMsg(usernameInput, "Username must be at least 4 characters long");
  } else {
    setSuccessMsg(usernameInput);
  }
}
function input1function() {
  let emailInput = document.getElementById("email");
  let email = emailInput.value;
  if (isEmail(email)) {
    setSuccessMsg(emailInput);
  } else {
    setErrorMsg(emailInput, "add proper email");
  }
}
function input2function() {
  let birthdaytimeInput = document.getElementById("birthdaytime");
  let birthdaytime = birthdaytimeInput.value;

  if (!birthdaytime) {
    setErrorMsg(birthdaytimeInput, "Date of birth cannot be blank");
  } else {
    setSuccessMsg(birthdaytimeInput);
  }
}
function input3function() {
  let phone_noInput = document.getElementById("phone_no");
  let phone_no = phone_noInput.value;

  if (isNaN(phone_no) || phone_no.length != 10) {
    setErrorMsg(phone_noInput, "Enter a valid 10-digit contact number");
  } else {
    setSuccessMsg(phone_noInput);
  }
}
function input4function() {
  let passwordInput = document.getElementById("password");
  let password = passwordInput.value;
  if (password.length < 8) {
    setErrorMsg(passwordInput, "Password must be at least 8 characters long");
  } else {
    setSuccessMsg(passwordInput);
  }
}
function handlechange() {
  let a = findselected();
  if (!a) {
    setErrorMsg(language[0], "select one atleast");
  } else {
    setSuccessMsg(language[0]);
  }
}
function handlechange1() {
  let a = check_data();
  if (!a) {
    setErrorMsg(check[0], "Select at least one Vehicle");
  } else {
    setSuccessMsg(check[0]);
  }
}
