<div class="container">
  <div class="header">
      <p class="title">Stefan Reifenberg</p>
      <div class="spacer"></div>
  </div>

  <div class="sub-header">
    <p class="sub-text">      
      <span>Freelance Information Designer</span> <br />
      <b>—</b>
  </p>
  </div>

  <div class="spacer-auto"></div>

  <div class="main-title">
      <p class="big-text-left">04</p>
      <div class="spacer-small"></div>
      <p class="big-text-right">2025</p>
  </div>

  <div class="spacer-auto"></div>

  <div class="footer">
      <p class="footer-text">
          <b>THREE.JS</b><br />
          3D JavaScript Library
      </p>
      <div class="spacer-small"></div>
      <p class="footer-title">FRONTEND MEETUP FREIBURG</p>
      <div class="spacer-small"></div>
      <p class="footer-empty"></p>
  </div>
</div>

<style>
  * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
  }

  .container {
      width: 100vw;
      min-height: 100vh;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      pointer-events: none;
      overflow: hidden;
  }

  .header, .footer {
      width: 100%;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
  }

  .title {
      font-family: "Antonio", sans-serif;
      font-size: 2rem;
      font-weight: 700;
      line-height: 1.2;
      color: black;
      letter-spacing: -2px;
  }

  .sub-header {
      width: 100%;
      display: flex;
      flex-direction: row;
      align-items: flex-start;
      justify-content: start;
  }

  .sub-text {
      font-size: 1rem;
      line-height: 1.5;
      color: black;
      text-align: left;
  }

  .main-title {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      width: 100%;
  }

  .big-text-left {
      font-size: clamp(6rem, 20vw, 12rem);
      line-height: 1;
      color: black;
      margin: 0;
      /* letter-spacing: -0.2em; */
      text-align: start;
      width: 100%;
  }
  .big-text-right {
      font-size: clamp(6rem, 20vw, 12rem);
      line-height: 1;
      color: black;
      margin: 0;
      text-align: end;
      width: 100%;
  }

  .footer {
      width: 100%;
      display: flex;
      flex-direction: row;
      align-items: flex-end;
      justify-content: stretch;
      pointer-events: all;
  }

  .footer-text {
      white-space: nowrap;
      font-size: 1rem;
      line-height: 1.5;
      color: black;
  }

  .footer-title {
      font-family: "Antonio", sans-serif;
      font-size: 1.2rem;
      font-weight: 700;
      text-align: center;
      color: black;
      letter-spacing: -0.05em;
      white-space: nowrap;
  }

  .footer-empty {
      font-size: 1rem;
      line-height: 1;
      text-align: right;
      color: black;
  }

  /* Flexible Spacing */
  .spacer {
      flex: 1;
  }

  .spacer-auto {
      flex-grow: 1;
  }

  .spacer-small {
      width: 0.5rem;
  }
</style>