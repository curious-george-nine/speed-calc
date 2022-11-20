<script>
  import { Button, Icon, TabPane } from "sveltestrap";

  let started = false;
  let counting = false;
  let result = false;

  const changeBool = (
    /** @type {Boolean} */ sta,
    /** @type {Boolean} */ cou,
    /** @type {Boolean} */ res
  ) => {
    started = sta;
    counting = cou;
    result = res;
  };

  const backToHome = () => {
    clickedAmount = 0;

    changeBool(false, false, false);
  };

  $: countdownNum = undefined;

  let clickingCountdown;
  let cCdNum = 10;
  let endClicking;
  let rate;

  $: clickedAmount = 0;

  const clickerClicked = () => {
    clickedAmount = clickedAmount + 1;
  };

  function startClick() {
    countdownNum = 3;

    counting = true;

    const startedEvent = () => {
      clickingCountdown = setInterval(() => {
        cCdNum--;

        console.log(cCdNum);
      }, 1000);

      endClicking = setTimeout(() => {
        clearInterval(clickingCountdown);
        console.log(clickedAmount);

        changeBool(false, false, true);

        if (clickedAmount <= 2) rate = "ナマケモノ";
        else if (clickedAmount <= 20) rate = "カメ";
        else if (clickedAmount <= 40) rate = "一般人";
        else if (clickedAmount <= 70) rate = "ゲーマー";
        else if (clickedAmount <= 120) rate = "プロゲーマー";
        else if (clickedAmount <= 150) rate = "天才";
        else if (clickedAmount <= 500) rate = "ハッカー";
        else if (clickedAmount == 1000) rate = "自動クリッカー";

        countdownNum = undefined;
        clickingCountdown = undefined;
        cCdNum = 10;
      }, 10000);
    };

    const countdown = setInterval(() => {
      countdownNum--;
    }, 1000);

    setTimeout(() => {
      clearInterval(countdown);
      changeBool(true, false, false);

      startedEvent();
    }, 3000);
  }

  function stopClick() {
    console.log("STOPPED! NOW STOP! JS PLS WORK!");
    clearInterval(clickingCountdown);
    clearTimeout(endClicking);

    changeBool(false, false, false);
    countdownNum = undefined;
    clickingCountdown = undefined;
    cCdNum = 10;
    clickedAmount = 0;
  }
</script>

<TabPane tabId="click" active>
  <span slot="tab">
    クリック <Icon name="cursor-fill" />
  </span>
  <h2 class="my-4 text-light">クリック計測</h2>
  {#if !counting && !started && !result}
    <div class="card clicker mx-auto p-4 mb-4">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="160"
        height="160"
        fill="currentColor"
        class="card-img"
        viewBox="0 0 16 16"
      >
        <path
          d="M6.75 1a.75.75 0 0 1 .75.75V8a.5.5 0 0 0 1 0V5.467l.086-.004c.317-.012.637-.008.816.027.134.027.294.096.448.182.077.042.15.147.15.314V8a.5.5 0 1 0 1 0V6.435a4.9 4.9 0 0 1 .106-.01c.316-.024.584-.01.708.04.118.046.3.207.486.43.081.096.15.19.2.259V8.5a.5.5 0 0 0 1 0v-1h.342a1 1 0 0 1 .995 1.1l-.271 2.715a2.5 2.5 0 0 1-.317.991l-1.395 2.442a.5.5 0 0 1-.434.252H6.035a.5.5 0 0 1-.416-.223l-1.433-2.15a1.5 1.5 0 0 1-.243-.666l-.345-3.105a.5.5 0 0 1 .399-.546L5 8.11V9a.5.5 0 0 0 1 0V1.75A.75.75 0 0 1 6.75 1zM8.5 4.466V1.75a1.75 1.75 0 1 0-3.5 0v5.34l-1.2.24a1.5 1.5 0 0 0-1.196 1.636l.345 3.106a2.5 2.5 0 0 0 .405 1.11l1.433 2.15A1.5 1.5 0 0 0 6.035 16h6.385a1.5 1.5 0 0 0 1.302-.756l1.395-2.441a3.5 3.5 0 0 0 .444-1.389l.271-2.715a2 2 0 0 0-1.99-2.199h-.581a5.114 5.114 0 0 0-.195-.248c-.191-.229-.51-.568-.88-.716-.364-.146-.846-.132-1.158-.108l-.132.012a1.26 1.26 0 0 0-.56-.642 2.632 2.632 0 0 0-.738-.288c-.31-.062-.739-.058-1.05-.046l-.048.002zm2.094 2.025z"
        />
      </svg>
      <div class="card-img-overlay" />
    </div>
    <br />
    <Button color="success" size="lg" on:click={startClick}>スタート!</Button>
  {:else if !counting && started && !result}
    <button style="display: contents" on:click={clickerClicked}>
      <div class="card clicker started mx-auto p-4 mb-4">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="160"
          height="160"
          fill="currentColor"
          class="card-img"
          viewBox="0 0 16 16"
        >
          <path
            d="M6.75 1a.75.75 0 0 1 .75.75V8a.5.5 0 0 0 1 0V5.467l.086-.004c.317-.012.637-.008.816.027.134.027.294.096.448.182.077.042.15.147.15.314V8a.5.5 0 1 0 1 0V6.435a4.9 4.9 0 0 1 .106-.01c.316-.024.584-.01.708.04.118.046.3.207.486.43.081.096.15.19.2.259V8.5a.5.5 0 0 0 1 0v-1h.342a1 1 0 0 1 .995 1.1l-.271 2.715a2.5 2.5 0 0 1-.317.991l-1.395 2.442a.5.5 0 0 1-.434.252H6.035a.5.5 0 0 1-.416-.223l-1.433-2.15a1.5 1.5 0 0 1-.243-.666l-.345-3.105a.5.5 0 0 1 .399-.546L5 8.11V9a.5.5 0 0 0 1 0V1.75A.75.75 0 0 1 6.75 1zM8.5 4.466V1.75a1.75 1.75 0 1 0-3.5 0v5.34l-1.2.24a1.5 1.5 0 0 0-1.196 1.636l.345 3.106a2.5 2.5 0 0 0 .405 1.11l1.433 2.15A1.5 1.5 0 0 0 6.035 16h6.385a1.5 1.5 0 0 0 1.302-.756l1.395-2.441a3.5 3.5 0 0 0 .444-1.389l.271-2.715a2 2 0 0 0-1.99-2.199h-.581a5.114 5.114 0 0 0-.195-.248c-.191-.229-.51-.568-.88-.716-.364-.146-.846-.132-1.158-.108l-.132.012a1.26 1.26 0 0 0-.56-.642 2.632 2.632 0 0 0-.738-.288c-.31-.062-.739-.058-1.05-.046l-.048.002zm2.094 2.025z"
          />
        </svg>
        <div class="card-img-overlay" />
      </div>
    </button>
    <Button color="danger" size="lg" on:click={stopClick}>やめる</Button>
  {:else if counting && !started && !result}
    <div class="card clicker mx-auto p-4 mb-4">
      <div class="fs-3">{countdownNum}</div>
    </div>
    <Button size="lg" disabled>スタート!</Button>
  {:else if !counting && !started && result}
    <div class="card clicker result mx-auto p-4 mb-4">
      <h3 class="fs-3">結果</h3>
      <p class="fs-5">
        {clickedAmount}クリック!
        <br />
        <span class="fs-6">
          毎秒{clickedAmount / 10}クリック
        </span>
      </p>
      <p class="fs-4">
        レベル: {rate}
      </p>
      <Button class="mt-3" on:click={backToHome}>閉じる</Button>
    </div>
  {/if}
</TabPane>

<style>
  .clicker {
    width: 20rem !important;
    height: 20rem !important;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .clicker.started:active {
    background-color: #ff0000;
  }
</style>
