# Portfolio README

## Overview

This is a personal portfolio website designed to showcase the projects and skills of Faraz Akhtar Khan. The portfolio highlights my academic and extracurricular projects, my skills in web development, and provides a means for potential employers and collaborators to contact me.

## Features

- **Typing Animation**: An animated typing effect to display different roles.
- **Responsive Navigation**: A collapsible navigation bar for better user experience on smaller screens.
- **Dynamic Sections**: Smooth transitions between different sections of the portfolio.
- **Contact Form**: A functional contact form that sends messages using EmailJS.
- **Download CV**: A button to download my resume.

## Technologies Used

- **HTML5**: For structuring the content.
- **CSS3**: For styling the website.
- **JavaScript**: For interactivity and dynamic content.
- **EmailJS**: For sending emails from the contact form.

## Getting Started

### Prerequisites

To run this project locally, you need to have a modern web browser.

### Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/FarazAkhtarKhan/portfolio.git
   ```

2. **Navigate to the project directory:**

   ```bash
   cd portfolio
   ```

3. **Open the `index.html` file in your browser:**

   ```bash
   open index.html
   ```

## Usage

### Typing Animation

The typing animation is initialized with the following script:

```javascript
var typed = new Typed(".typing", {
    strings: ["Developer"],
    typeSpeed: 100,
    backSpeed: 60,
    loop: true
});
```

### Navigation and Sections

The navigation bar allows users to switch between sections. The active section is highlighted, and a smooth transition is applied:

```javascript
const nav = document.querySelector(".nav"),
    navList = nav.querySelectorAll("li"),
    totalNavList = navList.length,
    allSection = document.querySelectorAll(".section"),
    totalSection = allSection.length;

for (let i = 0; i < totalNavList; i++) {
    const a = navList[i].querySelector("a");
    a.addEventListener("click", function () {
        removeBackSection();
        for (let j = 0; j < totalNavList; j++) {
            if (navList[j].querySelector("a").classList.contains("active")) {
                addBackSection(j);
            }
            navList[j].querySelector("a").classList.remove("active");
        }
        this.classList.add("active");
        showSection(this);

        if (window.innerWidth < 1200) {
            asideSectionTogglerBtn();
        }
    });
}

function removeBackSection() {
    for (let i = 0; i < totalSection; i++) {
        allSection[i].classList.remove("back-section");
    }
}

function addBackSection(num) {
    allSection[num].classList.add("back-section");
}

function showSection(element) {
    for (let i = 0; i < totalSection; i++) {
        allSection[i].classList.remove("active");
    }
    const target = element.getAttribute("href").split("#")[1];
    document.querySelector("#" + target).classList.add("active");
}

function updateNav(element) {
    for (let i = 0; i < totalNavList; i++) {
        navList[i].querySelector("a").classList.remove("active");
        const target = element.getAttribute("href").split("#")[1];
        if (target === navList[i].querySelector("a").getAttribute("href").split("#")[1]) {
            navList[i].querySelector("a").classList.add("active");
        }
    }
}

document.querySelector(".hire-me").addEventListener("click", function () {
    const sectionIndex = this.getAttribute("data-section-index");
    showSection(this);
    updateNav(this);
    removeBackSection();
    addBackSection(sectionIndex);
});

const navTogglerBtn = document.querySelector(".nav-toggler"),
    aside = document.querySelector(".aside");

navTogglerBtn.addEventListener("click", () => {
    asideSectionTogglerBtn();
});

function asideSectionTogglerBtn() {
    aside.classList.toggle("open");
    navTogglerBtn.classList.toggle("open");
    for (let i = 0; i < totalSection; i++) {
        allSection[i].classList.toggle("open");
    }
}
```

### Contact Form

The contact form uses EmailJS to send emails. Make sure to include the EmailJS SDK and initialize it with your user ID:

```html
<script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script type="text/javascript">
    (function() {
        emailjs.init("YOUR_USER_ID");
    })();
</script>
```

Handle the form submission:

```javascript
document.getElementById('contact-form').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent form from submitting normally

    const serviceID = 'your_service_id';
    const templateID = 'your_template_id';

    emailjs.sendForm(serviceID, templateID, this)
        .then(() => {
            alert('Message sent successfully!');
        }, (err) => {
            alert('Failed to send message: ' + JSON.stringify(err));
        });
});
```

### Download CV

To enable the CV download, link the CV file to the download button:

```html
<a href="path/to/your_cv.pdf" download="Faraz_Akhtar_Khan_CV.pdf" class="btn">Download CV</a>
```

## License

This project is licensed under the MIT License.

Thank you for checking out my portfolio! I hope you find it informative and engaging.
