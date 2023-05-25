<div class="page">
  <div class="header">
    <div class="header-box">
      <div class="logo">A</div>
    </div>
  </div>
</div>

<style>
  .page {
    cursor: crosshair;
  }
  .header {
    /*background: url("/bg4.png");*/
    background: white;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: bottom;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .header-box {
    background: var(--primary);
    color: var(--tertiary);
    border: 6px solid var(--tertiary);
    height: 160px;
    width: 160px;
    max-width: 100%;
    padding: 10px;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-transform: uppercase;
    font-family: monospace;
    font-weight: thin;
    font-family: monospace;
    border-radius: 10000px;
  }

  .header-box > .logo {
    font-size: 100px;
    font-family: "Major Mono Display", monospace;
    user-select: none;
    margin:0;
    line-height: 0;
    margin-bottom:20px;
  }


</style>