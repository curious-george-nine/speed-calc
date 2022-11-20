<script>
  // @ts-nocheck

  import { Button } from "sveltestrap";

  let color;

  const bodyElement = document.body;

  const mql = window.matchMedia("(prefers-color-scheme: dark)");

  if (localStorage.getItem("theme")) {
    color = localStorage.getItem("theme");
    bodyElement.classList.add(`bg-${color}`);

    document.querySelectorAll(`.text-dark`).forEach((el) => {
      el.classList.replace("text-dark", "text-light");
    });

    document.querySelectorAll(".text-light").forEach((el) => {
      el.classList.replace("text-light", "text-dark");
    });
  } else {
    // @ts-ignore
    color = mql.matches ? "dark" : "light";

    mql.matches
      ? bodyElement.classList.add("bg-dark")
      : bodyElement.classList.add("bg-light");
  }
  function clickEvent() {
    if (color === "dark") {
      color = "light";
      bodyElement.classList.add("bg-light");
      bodyElement.classList.remove("bg-dark");
      localStorage.setItem("theme", "light");

      document.querySelectorAll(".text-light").forEach((el) => {
        el.classList.replace("text-light", "text-dark");
      });
    } else {
      color = "dark";
      bodyElement.classList.add("bg-dark");
      bodyElement.classList.remove("bg-light");
      localStorage.setItem("theme", "dark");

      document.querySelectorAll(".text-dark").forEach((el) => {
        el.classList.replace("text-dark", "text-light");
      });
    }
  }

  bodyElement.style.transition = "background-color 0.3s";
</script>

<div class="position-absolute bottom-0 left-0">
  <Button {color} on:click={clickEvent}>
    現在: {color === "dark" ? "ダーク" : "ライト"}
  </Button>
</div>
