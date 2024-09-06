<script>
  import vfsg_logo from "../assets/vfsg_logo.png";
  import ns_logo from "../assets/noise_solution_logo.svg";
</script>

<div class="footer-container">
  <div>
    <p>A project made by Flore</p>
    <p>flore.dev</p>
  </div>
  <div class="partners">
    <img src={ns_logo} alt="Noise Solution logo" />
    <img src={vfsg_logo} alt="Viz for Social Good logo" />
  </div>
</div>

<style>
  .footer-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 20px;
    margin-top: 20px;
  }

  .footer-container > div {
    margin: 0 auto;
    text-align: center;
  }

  .footer-container .partners {
    display: flex;
    gap: 32px;
  }

  .footer-container .partners img {
    height: 80px;
  }
</style>
