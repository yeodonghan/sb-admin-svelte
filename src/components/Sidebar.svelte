<script>
  import Collapse from "sveltestrap/src/Collapse.svelte";
  import Nav from "sveltestrap/src/Nav.svelte";

  import SidebarItem from "./SidebarItem.svelte";

  export let segment;
  export let theme;

  $: sidenav_theme = `sb-sidenav-${theme}`;

  let isLayoutOpen = false;
  let isSettingOpen = false;
  let isPageOpen = false;
  let isAuthenticationOpen = false;
  let isErrorOpen = false;
  let activeLink = "Dashboard";
  let footerName = "";
  let footerText = "";

  const updateActiveLink = (linkName) => (activeLink = linkName);

  const toggleLayout = () => {
    isLayoutOpen = !isLayoutOpen;
    if (isPageOpen === true) isPageOpen = false;
  };

  const toggleSetting = () => {
    isSettingOpen = !isSettingOpen;
    if (isPageOpen === true) isPageOpen = false;
  };

  const togglePages = () => {
    isPageOpen = !isPageOpen;
    if (isLayoutOpen === true) isLayoutOpen = false;
    if (isPageOpen === false) {
      isAuthenticationOpen = false;
      isErrorOpen = false;
    }
  };

  const toggleAuthentication = () => {
    isAuthenticationOpen = !isAuthenticationOpen;
    if (isErrorOpen === true) isErrorOpen = false;
  };

  const toggleError = () => {
    isErrorOpen = !isErrorOpen;
    if (isAuthenticationOpen === true) isAuthenticationOpen = false;
  };
</script>

<div id="layoutSidenav_nav" class="sb-nav-fixed">
  <Nav
    class="sb-sidenav {sidenav_theme} accordion sb-nav-fixed"
    id="sidenavAccordion"
  >
    <div class="sb-sidenav-menu">
      <Nav>
        <div class="sb-sidenav-menu-heading">Home</div>
        <SidebarItem
          on:press={() => {
            theme = "dark";
          }}
          text="Dashboard"
          class={segment === "." || segment === undefined ? "active" : ""}
          leftIcon
          href="."
        >
          <i class="fas fa-tachometer-alt" slot="leftIcon" />
        </SidebarItem>

        <div class="sb-sidenav-menu-heading">Users</div>
        <SidebarItem
          class={segment === "users" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="users"
          text="Registered Users"
          leftIcon
        >
          <i class="fas fa-users" slot="leftIcon" />
        </SidebarItem>

        <div class="sb-sidenav-menu-heading">Quiz</div>
        <SidebarItem
          class={segment === "categories" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="categories"
          text="Categories"
          leftIcon
        >
          <i class="fas fa-book" slot="leftIcon" />
        </SidebarItem>
        <SidebarItem
          class={segment === "questions" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="questions"
          text="Questions"
          leftIcon
        >
          <i class="fas fa-trophy" slot="leftIcon" />
        </SidebarItem>
        <SidebarItem
          class={segment === "questionsreports" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="questionsreports"
          text="Questions Reports"
          leftIcon
        >
          <i class="fas fa-question-circle" slot="leftIcon" />
        </SidebarItem>

        <div class="sb-sidenav-menu-heading">Actions</div>
        <SidebarItem
          class={segment === "notifications" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="notifications"
          text="Send Notifications"
          leftIcon
        >
          <i class="fas fa-bullhorn" slot="leftIcon" />
        </SidebarItem>
        <SidebarItem
          class={segment === "importquestions" ? "active" : ""}
          on:press={() => {
            theme = "dark";
          }}
          href="importquestions"
          text="Import Questions"
          leftIcon
        >
          <i class="fas fa-download" slot="leftIcon" />
        </SidebarItem>
      </Nav>
    </div>

    <div class="sb-sidenav-footer">
      <div class="small">{footerText}</div>
      {footerName}
    </div>
  </Nav>
</div>
