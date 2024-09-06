<script>
  import vfsg_logo from "../assets/vfsg_logo.png";
  import ns_logo from "../assets/noise_solution_logo.svg";
</script>

<div class="footer-container">
  <div>
    <p>
      A project made by <a
        href="https://github.com/wildvariables"
        target="_blank">Flore</a
      >
    </p>
    <p>
      Code available <a
        href="https://github.com/wildvariables/vfsg-noise-solution"
        target="_blank">here</a
      >
    </p>
  </div>
  <div class="partners">
    <a href="https://www.noisesolution.org/" target="_blank"
      ><img src={ns_logo} alt="Noise Solution logo" /></a
    >
    <a href="https://www.vizforsocialgood.com/" target="_blank"
      ><img src={vfsg_logo} alt="Viz for Social Good logo" /></a
    >
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

  .footer-container a,
  .footer-container a:visited {
    color: white;
    text-decoration: underline white;
  }
</style>
