# car-part-replacements
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Car Parts Finder</title>
<style>
body {
font-family: Arial, sans-serif;
background-color: #f0f3f7;
padding: 40px;
text-align: center;
}

h1 {
color: #2c3e50;
}

select, button {
padding: 10px;
font-size: 16px;
margin: 10px;
}

#partInfo {
margin-top: 30px;
}

.link-button {
display: inline-block;
background-color: #3498db;
color: white;
padding: 10px 20px;
margin: 10px;
text-decoration: none;
border-radius: 6px;
}

.link-button:hover {
background-color: #2980b9;
}
</style>
</head>
<body>

<h1>Car Parts Finder</h1>

<label for="categorySelect">Choose a category:</label>
<select id="categorySelect" onchange="updateParts()">
<option value="">-- Select Category --</option>
<option value="engine">Engine</option>
<option value="brakes">Brakes</option>
<option value="tires">Tires</option>
<option value="suspension">Suspension</option>
<option value="interior">Interior</option>
</select>

<br>

<label for="partSelect">Choose a part:</label>
<select id="partSelect">
<option value="">-- Select Part --</option>
</select>

<br>

<button onclick="showPartInfo()">Find Part</button>

<div id="partInfo"></div>

<script>
const partsData = {
engine: {
"Spark Plug": {
links: {
Amazon: "https://www.amazon.com/s?k=spark+plug",
AutoZone: "https://www.autozone.com/ignition/spark-plug",
eBay: "https://www.ebay.com/sch/i.html?_nkw=spark+plug"
}
},
"Oil Filter": {
links: {
Amazon: "https://www.amazon.com/s?k=oil+filter",
RockAuto: "https://www.rockauto.com/en/catalog/*,oil+filter",
Walmart: "https://www.walmart.com/search?q=oil+filter"
}
}
},
brakes: {
"Brake Pads": {
links: {
Amazon: "https://www.amazon.com/s?k=brake+pads",
AutoZone: "https://www.autozone.com/brakes-and-traction-control/brake-pads",
OReilly: "https://www.oreillyauto.com/shop/b/brakes---wheel-bearings/brake-pads"
}
},
"Brake Rotors": {
links: {
eBay: "https://www.ebay.com/sch/i.html?_nkw=brake+rotors",
RockAuto: "https://www.rockauto.com/en/catalog/*,rotor",
Amazon: "https://www.amazon.com/s?k=brake+rotors"
}
}
},
tires: {
"All-Season Tires": {
links: {
TireRack: "https://www.tirerack.com/content/tirerack/desktop/en/tire-categories/all-season.html",
Walmart: "https://www.walmart.com/search?q=all+season+tires",
DiscountTire: "https://www.discounttire.com/tires/all-season"
}
},
"Snow Tires": {
links: {
Amazon: "https://www.amazon.com/s?k=snow+tires",
TireRack: "https://www.tirerack.com/content/tirerack/desktop/en/tire-categories/winter.html",
Costco: "https://tires.costco.com/"
}
}
},
suspension: {
"Shock Absorbers": {
links: {
RockAuto: "https://www.rockauto.com/en/catalog/*,shock+absorber",
Amazon: "https://www.amazon.com/s?k=shock+absorbers",
AutoZone: "https://www.autozone.com/suspension-steering-tire-and-wheel/shock-strut"
}
},
"Struts": {
links: {
eBay: "https://www.ebay.com/sch/i.html?_nkw=car+struts",
Amazon: "https://www.amazon.com/s?k=car+struts",
OReilly: "https://www.oreillyauto.com/shop/b/suspension---steering/strut-assembly"
}
}
},
interior: {
"Car Mats": {
links: {
Amazon: "https://www.amazon.com/s?k=car+mats",
WeatherTech: "https://www.weathertech.com/",
Walmart: "https://www.walmart.com/search?q=car+mats"
}
},
"Seat Covers": {
links: {
AutoZone: "https://www.autozone.com/interior-accessories/seat-cover",
eBay: "https://www.ebay.com/sch/i.html?_nkw=seat+covers",
Amazon: "https://www.amazon.com/s?k=seat+covers"
}
}
}
};

function updateParts() {
const category = document.getElementById("categorySelect").value;
const partSelect = document.getElementById("partSelect");
partSelect.innerHTML = '<option value="">-- Select Part --</option>';

if (category && partsData[category]) {
const parts = Object.keys(partsData[category]);
parts.forEach(part => {
const option = document.createElement("option");
option.value = part;
option.textContent = part;
partSelect.appendChild(option);
});
}
}

function showPartInfo() {
const category = document.getElementById("categorySelect").value;
const part = document.getElementById("partSelect").value;
const infoDiv = document.getElementById("partInfo");
infoDiv.innerHTML = "";

if (category && part && partsData[category][part]) {
const partInfo = partsData[category][part];
const heading = document.createElement("h3");
heading.textContent = `Buy "${part}" from:`;
infoDiv.appendChild(heading);

for (const [site, url] of Object.entries(partInfo.links)) {
const a = document.createElement("a");
a.href = url;
a.target = "_blank";
a.className = "link-button";
a.textContent = site;
infoDiv.appendChild(a);
}
} else {
infoDiv.innerHTML = "<p>Please select a valid category and part.</p>";
}
}
</script>

</body>
</html>
