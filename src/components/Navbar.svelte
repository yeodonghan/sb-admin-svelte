<script>
  import Navbar from "sveltestrap/src/Navbar.svelte";
  import NavbarBrand from "sveltestrap/src/NavbarBrand.svelte";
  import NavbarToggler from "sveltestrap/src/NavbarToggler.svelte";
  import Nav from "sveltestrap/src/Nav.svelte";
  import NavItem from "sveltestrap/src/NavItem.svelte";
  import NavLink from "sveltestrap/src/NavLink.svelte";
  import Collapse from "sveltestrap/src/Collapse.svelte";
  import UncontrolledDropdown from "sveltestrap/src/UncontrolledDropdown.svelte";
  import DropdownToggle from "sveltestrap/src/DropdownToggle.svelte";
  import DropdownMenu from "sveltestrap/src/DropdownMenu.svelte";
  import DropdownItem from "sveltestrap/src/DropdownItem.svelte";
  import ListGroup from "sveltestrap/src/ListGroup.svelte";
  import Form from "sveltestrap/src/Form.svelte";
  import InputGroup from "sveltestrap/src/InputGroup.svelte";
  import InputGroupAddon from "sveltestrap/src/InputGroupAddon.svelte";
  import Label from "sveltestrap/src/Label.svelte";
  import Input from "sveltestrap/src/Input.svelte";
  import CustomInput from "sveltestrap/src/CustomInput.svelte";
  import Button from "sveltestrap/src/Button.svelte";
  import { goto } from "@sapper/app";
  import { userInfo } from "../userStore.js";

  export let color;
  let auth = false;

  userInfo.subscribe((a) => (auth = a));

  const signOut = async () => {
    await fetch(
      "http://ec2-54-255-217-149.ap-southeast-1.compute.amazonaws.com:8000/api/logout",
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        credentials: "include",
      }
    );

    await goto("./pages/authentication/login");
  };

  function signOutHandler() {
    signOut();
  }
</script>

<Navbar class="sb-topnav navbar-expand" {color} dark expand="md">
  <NavbarBrand href=".">Admin</NavbarBrand>
  <Nav class="ml-auto" navbar>
    <ListGroup class="ml-auto ml-md-0">
      <UncontrolledDropdown nav inNavbar>
        <DropdownToggle nav caret>
          <i class="fas fa-user fa-fw ml-3" />
        </DropdownToggle>

        <DropdownMenu right>
          <DropdownItem divider />
          <DropdownItem>
            <Button class="dropdown-item" on:click={signOutHandler}
              >Logout</Button
            >
          </DropdownItem>
        </DropdownMenu>
      </UncontrolledDropdown>
    </ListGroup>
  </Nav>
</Navbar>
