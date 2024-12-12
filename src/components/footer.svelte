<!-- src/components/Footer.svelte -->
<script>
  // Optional: Add any interactive code or props if needed
</script>

<footer class="footer">
  <p class="footer-text">Made with ❤️ by Grover</p>
  <div class="footer-links">
    <a href="https://github.com/nishit2003/PulsePath" target="_blank" rel="noopener noreferrer">See Course Code</a>
    <a href="https://docs.google.com/document/d/1Qkmnb59ZncxB4BHhOTTnE4vMURVxmPz7VLR_0fzEnUo/edit?usp=sharingLinks to an external site.

" target="_blank" rel="noopener noreferrer">Docs</a>
    <a href="mailto:grovernt@mail.uc.edu" target="_blank" rel="noopener noreferrer">Contact Support</a>
  </div>
</footer>

<style>
  .footer {
    width: 100%;
    padding: 1rem;
    background-color: #f5ebe2;
    color: #927458;
    text-align: center;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    font-size: 0.9rem;
    /* position: fixed; */
    bottom: 0;
  }

  .footer-text {
    margin: 0;
    font-weight: bold;
  }

  .footer-links {
    margin-top: 0.5rem;
  }

  .footer-links a {
    color: #927458;
    text-decoration: none;
    margin: 0 0.5rem;
    font-weight: 500;
  }

  .footer-links a:hover {
    text-decoration: underline;
  }
</style>
