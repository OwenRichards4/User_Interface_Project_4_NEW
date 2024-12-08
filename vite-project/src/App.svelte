<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'

  let page = "main"
  let pageNum = 1;
  let totalRaised = 200;

  let includeCompany = false;
  let searchName = "";
  let first = "", last = "", email = "", connection = "", program = "", descrip = "", goal = 0, title = "" ;
  let editmode = false;
  let headerColor = "#c45888", buttonColor = "#80bf56", titleColor = "#c45888";
  let oldName, oldEmail, oldTitle, oldGoal, oldDescrip, oldTitleColor, oldHeaderColor, oldButtonColor;

  let events = [
    {
      firstname: "Owen",
      lastname: "Richards",
      email: "richaroc@mail.uc.edu",
      connection: "Other",
      program: "Research",
      descrip: "I would like to help anyone I can any way possible! The UC Rocket League club hosts a 24-hour charity match each year in January for Cincinnati Children's. So far, over the past 2 years, we've raised $3,500 and we hope to hit $5,000 total this January 17th-18th from 5pm-5pm. Our match will be live streamed with inncentives to the UCEsports twitch page at https://twitch.tv/ucesports. This is an actual event, so feel free to check it out!!",
      goal: 1000,
      title: "UC Rocket League 24-hour Charity Match"
    }
  ];
  let event = {};

  console.log(events)

  let infoShow = false

  function createEvent() {
    event = {
      firstname: first,
      lastname: last,
      email: email,
      connection: connection,
      program: program,
      descrip: descrip,
      goal: goal,
      title: title
    }

    page = "main";
    events.push(event);
    pageNum = 1
    first = ""
    last = ""
    email = ""
    connection = ""
    program = ""
    descrip = ""
    goal = 0
    title = ""
  }

  function searchEvent(val) {
    if (val != ""){
      events.forEach(element => {
        if (element.firstname.toUpperCase() == val.toUpperCase() || element.lastname.toUpperCase() == val.toUpperCase())  {
          page = "events"
          title = element.title;
          first = element.firstname;
          email = element.email;
          descrip = element.descrip;
          goal = element.goal;
        }
      });
    }
  }

  function createPage(val) {
    if (val == "create2024page") {
      page = "create2024page"
    } else {
      page = "main"
    }
  }

  function nextPage(val) {
    pageNum += 1;
    if (pageNum == 4) {
      pageNum = 1;
    }
  }

  function backAPage(val) {
    pageNum -= 1;
  }

  function showInfo() {
    if (infoShow) {
      infoShow = false
    } else {
      infoShow = true
    }
  }

  function go2editmode() {
    if (page == "events") {
      editmode = true
    }
    oldName = first;
    oldEmail = email;
    oldTitle = title;
    oldGoal = goal;
    oldDescrip = descrip;
    oldTitleColor = titleColor;
    oldHeaderColor = headerColor;
    oldButtonColor = buttonColor;
  }

  function exitEditMode(type) {
    if (type == 'exit') {
      first = oldName;
      email = oldEmail;
      title = oldTitle;
      goal = oldGoal;
      descrip = oldDescrip;
      titleColor = oldTitleColor;
      headerColor = oldHeaderColor;
      buttonColor = oldButtonColor;
    }
    editmode = false;
  }
</script>

<header>
  <ul>
    <a class="home-ul" href="" on:click={page == "main"}>Event Page Home</a>
    <a class="donate-ul" href="https://give.cincinnatichildrens.org/site/Donation2?df_id=1579&mfc_pref=T&1579.donation=form1&idb=0&set.SingleDesignee=1012&utm_source=marketing+site&utm_medium=button&utm_campaign=home+page">Donate Now</a>
    <a href="https://www.cincinnatichildrens.org/schedule-appointment">Schedule an appointment</a>
    <a href="https://www.cincinnatichildrens.org/locations">Directions</a>
    <a href="https://www.cincinnatichildrens.org/patients/visit/international">International</a>
    <a href="https://www.cincinnatichildrens.org/patient-resources/billing">Billing</a>
    <a href="https://mychart.cincinnatichildrens.org/mychart/Authentication/Login?">Sign in to MyChart</a>
    <a href="https://www.cincinnatichildrens.org/giving">Ways to help</a>
    <a href="https://www.cincinnatichildrens.org/">Patients and Family</a>
    <a href="https://www.cincinnatichildrens.org/professional">Healthcare Professionals</a>
    <a href="https://www.cincinnatichildrens.org/research">Researchers</a>
    <a href="https://www.cincinnatichildrens.org/search?start=0&site=entire-site">Search</a>
  </ul>
  <img src="src/assets/childrens-logo-new.png" alt="Cincinnati Children's Logo" style="position: relative; left: 60px;">
</header>
<div class="pre-main">
  <h2 style="color: rgb(196, 88, 136)">Giving Hope to Kids!</h2>
  <div class="login-details">
    <label for="username-input">Login:</label>
    <input id="username-input" type="text" placeholder="username">
    <input id="password-input" type="password" placeholder="password">
    <button>Sign In</button>
    <button id="remember-sign-in" type="checkbox"></button>
    <label for="remember-sign-in">Remember me?</label>
    <a class="link" href="">Trouble Signing In?</a>
  </div>
</div>
{#if editmode == false}
<main>
  {#if page == "main"}
    <div style="text-align: center;">
      <div class="title-and-info">
        <h1>Create an Online Fundraising Page for Cincinnati Children's</h1>
        <p>
          Host your own personal fundraising page – it’s a fun way to spread the word and raise money to help change the outcome for our patients and families.
        </p> 
      </div>
      <div class="event-creation-options">
        <div class="event-2024">
          <h2>2024 Event/Fundraiser</h2>
          <button on:click={() => createPage("create2024page")}>Create a 2024 Fundraising Page</button>
          <button>Create a 2024 Team Fundraising Page</button>
          <button>Join a Team for 2024 Fundraising</button>
          <button>Create a Fundraising Page for our College Hill Campaign</button>
        </div>
        <div class="future-event">
          <h2>Future Year Event/Fundraiser</h2>
          <button>Create an Ongoing Fundraising Page</button>
          <button>Create an Ongoing Team Fundraising Page</button>
          <button>Join a Team for Ongoing Fundraising</button>
        </div>
      </div>
      <p>To register a fundraiser without creating an online page, please <a class="link" href="https://www.shecodes.io/">click here</a>.</p>
      <div class="divider"></div>
      <div class="search">
        <h1>Search for a Event/Fundraiser</h1>
        <label for="name-search">To search for someone participating in this event or a team of participants, enter all or part of the name in this field:</label>
        <input id="name-search" type="text" placeholder="name" bind:value={searchName}>
        <button on:click={() => searchEvent(searchName)}>Search</button>
      </div>

      <p>If you have questions or would like more information, please email Andrew Stallings at <a class="link" href="">andrew.stallings@cchmc.org</a> or call 513-636-2915.</p>
    </div>
  {:else if page == "create2024page"}
    <div class="sequence">
      {#if pageNum == 1}
        <p class="num">1</p>
      {:else}
        <p class="grayNum">1</p>
      {/if}
      <p>Event Details</p>
      {#if pageNum == 2}
        <p class="num">2</p>
      {:else}
        <p class="grayNum">2</p>
      {/if}
      <p>Further Information</p>
      {#if pageNum == 3}
        <p class="num">3</p>
      {:else}
        <p class="grayNum">3</p>
      {/if}
      <p>Review</p>
    </div>
    <div class="participation">
      {#if pageNum == 1}
        <section>
          <label for="event-options" style="position: relative; font-size: 130%; font-weight: bold; top: 10px; color: rgb(196, 88, 136);">Select a Participation Type *</label>
          <ul class="event-options">
            <li class="event-option">
              <input type="radio" name="question0" value="event" />Celebration Page
              <p class="descrip">Have a birthday, anniversary or other milestone to celebrate? Personalize your own web page for your celebration.</p>
            </li>
            <li class="event-option">
              <input type="radio" name="question0" value="donation" />Donation Page
              <p class="descrip">Host your own personal fundraising page for any reason! Sign up for this online-only page to raise support for Cincinnati Children's.</p>
            </li>
            <li class="event-option">
              <input type="radio" name="question0" value="celebrate" />Event Page
              <p class="descrip">Host a donation page for an upcoming virtual or in-person fundraising event.</p>
            </li>
            <li class="event-option">
              <input type="radio" name="question0" value="honor" />Honor or Memorial Page
              <p class="descrip">Remarkable people enter our lives and change us in ways we never could have imagined. Recognize a special person in a simple and impactful way.</p>
            </li>
          </ul>
        </section>
        <section>
          <label for="goal" style="font-weight: bold; color: rgb(196, 88, 136); font-size: 120%">Fundraising Goal</label>
          <input class="goal" type="number" placeholder="Suggested: $100.00" bind:value={goal}>
        </section>
        <br><br>
        <section>
          <p>Would you like to make an additional gift?</p>
          <label for="additional-gift" style="font-weight: bold; color: rgb(196, 88, 136); font-size: 120%;">Other gift amount</label>
          <input class="goal" type="text">
          <br><br>
          <input class="company-name" type="checkbox" bind:checked={includeCompany}>
          <label for="company-name">Would you like to associate your participation with a company? You're welcome to remain anonymous if you prefer.</label>
          {#if includeCompany == true}
            <br><br>
            <input type="text" placeholder="Cincinnat Childrens...">
          {/if}
        </section>
        <section>
          <button on:click={() => nextPage(2)} class="nextpage" style="float: right; margin-right: 50px;">Next</button>
        </section>
      {:else if pageNum == 2}
        <div class="name-info">
          <h3 style="font-weight: bold; color: rgb(196, 88, 136); font-size: 120%">Name</h3>
          <section>
            <label for="firstname">First</label>
            <input id="firstname" type="text" bind:value={first}>
          </section>
          <section>
            <label for="lastname">Last</label>
            <input id="lastname" type="text" bind:value={last}>
          </section>
        </div>
        <h3 style="font-weight: bold; color: rgb(196, 88, 136); font-size: 120%">Contact Information</h3>
        <div class="contact-info">
          <section style="display: flex; flex-direction: column; gap: 10px; justify-content: start;">
            <section>
              <label for="street1">Street 1</label>
              <input id="street1" type="text">
            </section>
            <section>
              <label for="street2">Street 2</label>
              <input id="street2" type="text">
            </section>
            <section>
              <label for="street3">Street 3</label>
              <input id="street3" type="text">
            </section>
            <section>
              <label for="city">City / Town</label>
              <input id="city" type="text">
            </section>
            <section>
              <label for="state">State / Province</label>
              <input id="state" type="text">
            </section>
            <section>
              <label for="zip">ZIP / Postal Code</label>
              <input id="zip" type="text">
            </section>
          </section>
          <section style="display: flex; flex-direction: column; gap: 10px; justify-content: start;">
            <label for="country">Country</label>
            <input id="country" type="text">
            <label for="email">Email</label>
            <input id="email" type="text" bind:value={email}>
            <label for="phoneNumber">Phone Number</label>
            <input id="phoneNumber" type="text">
          </section>
        </div>
        <div class="addi-info">  
          <h3 style="font-weight: bold; color: rgb(196, 88, 136); font-size: 120%">Additional Information</h3>
          <section>
            <label for="connection">What is your connection to Cincinnati Children's?</label>
            <select id="connection" name="connection" bind:value={connection}>
              <option value="">Please select response</option>
              <option value="volvo">Parent of Patient</option>
              <option value="saab">Grandparent of Patient</option>
              <option value="fiat">Relative/Friend of Patient</option>
              <option value="audi">Patient</option>
              <option value="audi">Current Employee</option>
              <option value="audi">Former Employee</option>
              <option value="audi">Relative/Friend of Employee</option>
              <option value="audi">Contractor</option>
              <option value="audi">Auxiliary Member</option>
            </select>
          </section>
          <section>
            <label for="program">What program would you like your fundraising dollars to support?</label>
            <select id="program" bind:value={program}>
              <option value="">Please select response</option>
              <option value="greatest-needs">Greatest Needs</option>
              <option value="aaron-perlman-center">Aaron Perlman Center</option>
              <option value="bmcp">Behavioral Medicine and Clinical Psychology (BMCP)</option>
              <option value="cbdi">Cancer and Blood Diseases Institute (CBDI)</option>
              <option value="cced">CCED (Cincinnati Center for Eosinophilic Disorders)</option>
              <option value="charitable-care-fund">Charitable Care Fund</option>
              <option value="child-life-integrative-care">Child Life & Integrative Care</option>
              <option value="ddbp">Division of Developmental & Behavioral Pediatrics (DDBP)</option>
              <option value="gastroenterology">Gastroenterology</option>
              <option value="heart-institute">Heart Institute</option>
              <option value="human-genetics">Human Genetics</option>
              <option value="nephrology">Nephrology</option>
              <option value="neurology">Neurology</option>
              <option value="ot-pt">Occupational/Physical Therapy (OT/PT)</option>
              <option value="orthopaedics">Orthopaedics</option>
              <option value="perinatal-institute">Perinatal Institute</option>
              <option value="psychiatry">Psychiatry</option>
              <option value="research">Research</option>
              <option value="sickle-cell-research">Sickle Cell Research</option>
              <option value="starshine-hospice">StarShine Hospice</option>
            </select>
          </section>
          <section>
            <label for="program-other">If you've selected "Other" or would like to support a specific fund in the division chosen above, please specify the program/fund you would like your fundraising dollars to support:</label>
            <input id="program-other" type="text">
          </section>
          <label for="passion">Describe your event:</label>
          <textarea contenteditable="true" style="position: relative; height: 50px;" id="passion" type="text" bind:value={descrip}></textarea>
          <section>
            <input id="calendar" type="checkbox">
            <label for="calendar">I would like my event information may be included online or on printed hospital calendars.</label>
          </section>
          <section>
            <button on:click={() => backAPage(2)} class="nextpage" style="float: left; margin-right: 50px; background-color: rgb(196, 88, 136); width: 11%;">Go Back</button>
            <button on:click={() => nextPage(2)} class="nextpage" style="float: right; margin-right: 50px;">Next</button>
          </section>
        </div>
      {:else if pageNum == 3}
        <p>First Name: {first}</p>
        <p>Last Name: {last}</p>
        <p>Contact Email: {email}</p>
        <p>Connection: {connection}</p>
        <p>Desired Donation Program: {program}</p>
        <p>Description: {descrip}</p>
        <section>
          <button on:click={() => backAPage(2)} class="nextpage" style="float: left; margin-right: 50px; background-color: rgb(196, 88, 136); width: 11%;">Go Back</button>
          <button on:click={() => createEvent()} class="nextpage" style="float: right; margin-right: 50px;">Create Event</button>
        </section>
      {/if}
    </div>
  {:else if page == "events"}
    <div class="event-pages">
      <h1 style="text-align: center; font-size: 275%; color:{titleColor};">{title}</h1>
      <img src="src/assets/PC_banner_v2.jpg">
      <div class="flex-info-and-donation">
        <div>
          <section style="display:flex; align-items: center; gap: 10px;">
            <h3 style="color: {headerColor};">Director: </h3>
            <p style="font-size: 120%;">{first}</p>
          </section>
          <section style="display:flex; align-items: center; gap: 10px;">
            <h3 style="color: {headerColor};">Contact: </h3>
            <p style="font-size: 120%;">{email}</p>
          </section>
        </div>
        <div style="width: 20%;">
          <h3 style="position: relative; top: 25px; text-align: center; color: {headerColor}; font-size: 150%;">Progress</h3>
          <section style="position: relative; display: flex; justify-content: space-between; width: 100%; top: 15px;">
            <h2 style="color: {headerColor};">${totalRaised}</h2>
            <h2 style="color: {headerColor};">${goal}</h2>
          </section>
          <progress value={totalRaised} max={goal}></progress>
          <button style="background-color: {buttonColor};">Donate Now</button>
        </div>
      </div>
      <h3 style="color: {headerColor}">Information:</h3>
      <p style="position: relative; bottom: 15px; font-size: 110%;">{descrip}</p>

      <h3 style="color: {headerColor}">For the Cause</h3>
      <p style="position: relative; bottom: 15px; font-size: 110%;">Giving Hope, Cincinnati Children's community philanthropy program, is a great way to get involved and really make a difference for sick and injured kids. As a nonprofit hospital and medical center, Cincinnati Children's depends largely on support from the community.<br><br>By making a gift to my Giving Hope online fundraiser, you are helping to bring hope and healing to kids and families in our community, across the country and around the world.<br><br>Thank you! Together, we will change the outcome!</p>
      
      <h3 style="color: {headerColor}">Leave a comment</h3>
      <textarea style="position: relative; height: 150px; font-size: 120%;" placeholder="Add a comment..."></textarea>
      <button style="float: right;">Add Comment</button>
    </div>
    <div class="edit-button" on:click={() => go2editmode()}>
      <img style="position: relative; display: block; margin: auto; top: 8px;" src="src/assets/edit.png" width=30px>
    </div>
  {/if}
</main>
{:else}
  <main style="position: relative; left: 15%;">
    <div class="event-pages">
      <h1 style="text-align: center; font-size: 275%; color:{titleColor};">{title}</h1>
      <img src="src/assets/PC_banner_v2.jpg">
      <div class="flex-info-and-donation">
        <div>
          <section style="display:flex; align-items: center; gap: 10px;">
            <h3 style="color: {headerColor};">Director: </h3>
            <p style="font-size: 120%;">{first}</p>
          </section>
          <section style="display:flex; align-items: center; gap: 10px;">
            <h3 style="color: {headerColor};">Contact: </h3>
            <p style="font-size: 120%;">{email}</p>
          </section>
        </div>
        <div style="width: 20%;">
          <h3 style="position: relative; top: 25px; text-align: center; color: {headerColor}; font-size: 150%;">Progress</h3>
          <section style="position: relative; display: flex; justify-content: space-between; width: 100%; top: 15px;">
            <h2 style="color: {headerColor};">${totalRaised}</h2>
            <h2 style="color: {headerColor};">${goal}</h2>
          </section>
          <progress value={totalRaised} max={goal}></progress>
          <button style="background-color: {buttonColor};">Donate Now</button>
        </div>
      </div>
      <h3 style="color: {headerColor}">Information:</h3>
      <p style="position: relative; bottom: 15px; font-size: 110%;">{descrip}</p>

      <h3 style="color: {headerColor}">For the Cause</h3>
      <p style="position: relative; bottom: 15px; font-size: 110%;">Giving Hope, Cincinnati Children's community philanthropy program, is a great way to get involved and really make a difference for sick and injured kids. As a nonprofit hospital and medical center, Cincinnati Children's depends largely on support from the community.<br><br>By making a gift to my Giving Hope online fundraiser, you are helping to bring hope and healing to kids and families in our community, across the country and around the world.<br><br>Thank you! Together, we will change the outcome!</p>
      
      <h3 style="color: {headerColor}">Leave a comment</h3>
      <textarea placeholder="Add a comment..."></textarea>
    </div>
    <div class="edit-button" on:click={() => go2editmode()}>
      <img style="position: relative; display: block; margin: auto; top: 8px;" src="src/assets/edit.png" width=30px>
    </div>
  </main>
  <div class="edit-mode">
    <h3 style="font-size: 140%; text-decoration: underline;">You are in edit mode!</h3>
    <section>
      <label for="firstname-edit">First:</label>
      <input id="firstname-edit" type="text" bind:value={first}>
    </section>
    <section>
      <label for="email-edit">Email:</label>
      <input id="email-edit" type="text" bind:value={email}>
    </section>
    <section>
      <label for="title-edit">Title:</label>
      <input id="title-edit" type="text" bind:value={title}>
    </section>
    <section>
      <label for="goal-edit">Goal:</label>
      <input class="goal-edit" id="goal-edit" type="number" placeholder="Suggested: $100.00" bind:value={goal}>
    </section>
    <label for="passion-edit">Describe your event:</label>
    <textarea contenteditable="true" style="position: relative; height: fit-context; bottom: 15px;" id="passion-edit" type="text" bind:value={descrip}></textarea>
    <h3>Colors</h3>
    <section>
      <label for="headers">Title Color:</label>
      <input type="color" id="headers" bind:value={titleColor}>
    </section>
    <section>
      <label for="headers">Header Color:</label>
      <input type="color" id="headers" bind:value={headerColor}>
    </section>
    <section>
      <label for="headers">Button Color:</label>
      <input type="color" id="headers" bind:value={buttonColor}>
    </section>

    <button style="background-color: rgb(196, 88, 136); width: 75%; padding: 5px; align-self: center;" on:click={() => exitEditMode('save')}>Save and Exit</button>
    <button style="background-color: rgb(196, 88, 136); width: 75%; padding: 5px; align-self: center; margin-bottom: 10px;" on:click={() => exitEditMode('exit')}>Exit without Saving</button>
  </div>
{/if}
<footer>
  <h3 style="position: relative; text-align: center; color: rgb(196, 88, 136); font-size: 150%;">Connect with Us</h3>
  <ul>
    <a href="https://www.facebook.com/cincinnatichildrensfans">
      <img width=25px src="src/assets/facebook.png">
    </a>
    <a href="https://www.instagram.com/cincychildrens/">
      <img width=25px src="src/assets/instagram.png">
    </a>
    <a href="https://x.com/CincyChildrens">
      <img width=40px src="src/assets/X.png">
    </a>
    <a href="https://www.pinterest.com/cincychildrens/">
      <img width=25px src="src/assets/pinterest.png">
    </a>
    <a href="https://www.youtube.com/user/CincinnatiChildrens">
      <img width=55px src="src/assets/youtube.png">
    </a>
    <a href="https://blog.cincinnatichildrens.org/?_gl=1*jm2y2w*_ga*MjAyMTM5MzQ5LjE3MzI4MDc5NjY.*_ga_6ME8JGKTYE*MTczMzY2ODk4NS43LjEuMTczMzY2OTg1NC4wLjAuMA..">Patients and Family Blog</a>
    <a href="https://scienceblog.cincinnatichildrens.org/?_gl=1*jm2y2w*_ga*MjAyMTM5MzQ5LjE3MzI4MDc5NjY.*_ga_6ME8JGKTYE*MTczMzY2ODk4NS43LjEuMTczMzY2OTg1NC4wLjAuMA..">Research Blog</a>
  </ul>
  <div class="footer-nav">
    <div style="color: rgb(196, 88, 136)" class="quick-links">
      <h3>Quick Links</h3>
      <a href="">Schedule an Appointment</a>
      <a href="">Make a Referral</a>
      <a href="">Find an Urgent Care</a>
      <a href="">Find a Doctor / Researcher</a>
      <a href="">Pay a Bill</a>
      <a href="">Sign In to MyChart</a>
      <a href="">Request Medical Records</a>
    </div>
    <div style="color: rgb(196, 88, 136)" class="explore">
      <h3>Explore</h3>
      <a href="">Locations and Directions</a>
      <a href="">Clinical Services</a>
      <a href="">Conditions and Treatments</a>
      <a href="">Visitor and Patient Information</a>
      <a href="">Clinical Trials</a>
      <a href="">Events</a>
      <a href="https://give.cincinnatichildrens.org/site/SSurvey?ACTION_REQUIRED=URI_ACTION_USER_REQUESTS&SURVEY_ID=1660&utm_source=luminate&utm_medium=footer">Subscribe</a>
    </div>
    <div style="color: rgb(196, 88, 136)" class="about-us">
      <h3>About Us</h3>
      <a href="">About Cincinnati Children's</a>
      <a href="">Careers</a>
      <a href="">Newsroom</a>
      <a href="">Contact Us</a>
      <a href="">Download Our Caren App</a>
      <a href="">Terms of Use / Privacy Policies</a>
      <a href="">Non-Discrimination Notice</a>
    </div>
  </div>
  <div class="footer-end">
    <img src="src/assets/arc-pattern-lower-left.png">
    <p>
      3333 Burnet Avenue, Cincinnati, Ohio 45229-3026 | 1-513-636-4200 | 1-800-344-2462 <br><br>
      © Cincinnati Children's Hospital Medical Center. All rights reserved. <br><br>
      Cincinnati Children's is a tax-exempt 501(C)(3) nonprofit organization. Your gift is tax-deductible as allowed by law.
    </p>
    <a href="">
      <img src="src/assets/Badge-ChildrensHospitals-Honor-Roll_Generic-year86.png">
    </a>
    <a href="">
      <img src="src/assets/bptw.png">
    </a>
    <img src="src/assets/arc-pattern-upper-right.png" style="position: relative; bottom: 200px;">
  </div>
</footer>
{#if infoShow == true}
  <ul class="nextsteps">
    <h3>What to do next?</h3>
    <li>
      <h4 style="margin-bottom:5px; padding: 0;">Set up your Personal Page</h4>
      <p style="position: relative; margin-top: 0; left: 1px;">Customize your Personal Page with a story about why you are raising funds for this cause.</p>
    </li>
    <li>
      <h4 style="margin-bottom:5px; padding: 0;">Send an Email</h4>
      <p style="position: relative; margin-top: 0; left: 1px;">You have sent no emails to your family or friends. Add them to your Address Book and email them about your fundraising effort.</p>
    </li>
    <li>
      <h4 style="margin-bottom:5px; padding: 0;">Thank your Donors</h4>
      <p style="position: relative; margin-top: 0; left: 1px;">Thank your donors!</p>
    </li>
    <li>
      <h4 style="margin-bottom:5px; padding: 0;">Set a Goal</h4>
      <p style="position: relative; margin-top: 0; left: 1px;">Make sure to set your goal! Can you set an even higher goal?</p>
    </li>
    <li>
      <h4>Want to make some Changs?</h4>
      <section style="display: flex;">
        <img src="src/assets/edit-button.png">
        <p>Click this button on the bottom right of your event page to start editing!</p>
      </section>
    </li>
  </ul>
{/if}
{#if page == "events"}
<button class="information" on:click={() => showInfo()}>i</button>
{/if}



<style>
  :global(body) {
    margin: 0;
    padding: 0;

    font-family: "Gill Sans", sans-serif;

    margin: 0;
  }

  header {
    position: relative;

    margin-top: 30px;
    padding: 0px 30px;
  }

  header ul {
    position: relative;
    margin: 0;
    padding: 0;

    float: right;
    bottom: 30px;
    left: 30px;

    /*font-weight: bold;*/

    background-color: rgb(235, 235, 235);
  }

  ul a {
    position: relative;
    
    padding: 5px 15px;

    color: black;
    text-decoration: none;
  }

  ul {
    position: relative;
    display: flex;
    flex-direction: row;

    height: fit-content;
  }

  ul a:hover {
    background-color: rgb(220, 220, 220);
  }

  .pre-main, main {
    position: relative;
    width: 80%;
    left: 10%;
  }

  .pre-main {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;

    margin-bottom: 5px;
  }
  
  .login-details {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 5px;
  }

  .login-details input, .login-details button {
    padding: 5px;
  }

  .login-details label {
    font-size: 120%;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    gap: 20px;

    box-shadow: 1px 1px 8px rgb(10,10,10);
    padding: 10px 20px;

    margin-bottom: 30px;
  }

  main button {
    padding: 15px 30px;
    background-color: rgb(128, 191, 86);
    color: white;
    font-size: 100%;
    width: 100%;

    border: none;
    cursor: pointer;
  }

  main button:hover {
    background-color: rgb(112, 168, 76);
  }

  main h2 {
    color: rgb(196, 88, 136);
  }

  .event-creation-options {
    position: relative;

    display: flex;
    flex-direction: row;
    align-items: start;
    gap: 8%;
    
    justify-content: center;
  }

  .event-2024, .future-event {
    position: relative;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px;
    width: 30%;
  }

  .link {
    color: rgb(8, 167, 196);
    text-decoration: none;

    font-weight: bold;
  }

  .divider {
    position: relative;
    margin: 20px 0px;
    width: 90%;

    height: 1px;

    background-color: lightgray;
    left: 5%;
    bottom: 10px;
  }

  .search button {
    margin-top: 5px;
    width: 65%;
  }

  footer ul {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }

  .footer-nav {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: start;
    gap: 40px;
  }

  .quick-links, .explore, .about-us {
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .quick-links a, .explore a, .about-us a {
    color: gray;
    line-height: 30px;
    text-decoration: none;
  }

  .footer-end {
    position: relative;
    top: 50px;

    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .num {
    background-color: rgb(128, 191, 86);;
    padding: 10px 15px;
    border-radius: 40px;
  }

  .grayNum {
    background-color: lightgray;
    padding: 10px 15px;
    border-radius: 40px;
  }

  .sequence {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .event-options {
    display: flex;
    flex-direction: column;
    align-items: start;
    list-style: none;
  }
  
  .event-option {
    position: relative;
    padding: 10px;
    border: white solid 2px;
    right: 53px;
    padding-right: 40px;
  }

  .event-option:hover {
    background-color: rgb(245, 245, 245);
    border: rgb(196, 88, 136) solid 2px;
    border-radius: 10px;
  }

  .participation {
    border: 2px solid rgb(235, 235, 235, 1);
    margin: 0px 0px 20px 0px;
    padding: 20px;
    width: 75%;
    align-self: center;

    display: flex;
    flex-direction: column;
    justify-content: space-evenly;

  }

  .descrip {
    position: relative;

    color: gray;
    font-size: 80%;
    left: 22px;
  }

  .nextpage {
    width: 10%;
  }

  .information {
    position: fixed;
    bottom: 10px;
    right: 10px;
    
    background-color: rgb(128, 191, 86);
    padding: 10px 20px;
    border-radius: 50px;
    color: white;
    font-size: 150%;
    border: rgb(235, 235, 235) 3px solid;
  }
  .information:hover {
    background-color: rgb(112, 168, 76);
  }

  .nextsteps {
    position: fixed;
    bottom: -5px;
    right: 10px;

    width: 15%;
    background-color: white;
    padding: 10px;
    border: rgb(235, 235, 235) 3px solid;
    border-radius: 30px;

    display: flex;
    flex-direction: column;
    gap: 0px;

    list-style: none;
    line-height: 20px;
  }

  .nextsteps li {
    width: 100%;
    border-top: 2px solid rgb(235, 235, 235);
  }

  .donate-ul {
    background-color: rgb(196, 88, 136);
    color: white;
    font-weight: bolder;
  }

  .donate-ul:hover {
    background-color: rgb(176, 77, 121);
  }

  .home-ul {
    background-color: rgb(112, 168, 76); 
    color: white; 
    font-weight: bold;
  }

  .home-ul:hover {
    background-color: rgb(93, 140, 63);
  }

  .name-info {
    display: flex; 
    flex-direction: column; 
    gap: 10px;

    margin-bottom: 20px;
  }

  .contact-info {
    display: flex; 
    flex-direction: row; 
    gap: 50px;

    margin-bottom: 20px;
  }

  .addi-info {
    display: flex; 
    flex-direction: column; 
    gap: 20px;

    margin-bottom: 20px;
  }

  .name-info h3, .contact-info h3, .addi-info h3{
    margin-bottom: 0;
    padding-bottom: 0;
  }

  .event-pages {
    position: relative;

    width: 80%;
    left: 10%;

    display: flex;
    flex-direction: column;
    gap: 5px;
    justify-content: space-evenly;
  }

  .event-pages h3 {
    padding: 0;
    margin: 0;
  }

  progress {
    border: black solid 2px;
    width: 100%;
    margin-bottom: 20px;
  }

  progress::-webkit-progress-bar {
    background-color: white;
  }

  progress::-webkit-progress-value {
    background-color: rgb(128, 191, 86);
  }

  .flex-info-and-donation {
    display: flex;
    justify-content: space-between;

  }

  .edit-button {
    position: relative; 
    left: 97.4%; 

    background-color: rgb(128, 191, 86);

    width: 50px; 
    height: 50px; 
    border-radius: 10px;
  }

  .edit-button:hover {
    background-color: rgb(112, 168, 76);
    cursor: pointer;
  }

  .edit-mode {
    position: absolute;
    bottom: 5px;

    top: 25.2%;
    left: 0;
    width: 12%;
    height: fit-content;
    text-align: center;

    background-color: white;
    box-shadow: 1px 1px 8px rgb(10,10,10);

    padding: 5px 20px;

    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: start;
    gap: 20px;
  }

</style>