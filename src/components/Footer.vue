<template>
  <footer class="footer">
    <div class="footer-main">
      <div class="footer-left">
        <div class="footer-title">Amadeus IT Group</div>
        <div class="footer-address">
          C. Salvador de Madariaga, 1<br />
          28027 Madrid<br />
          Spain
        </div>
      </div>
      <div class="footer-right">
        <span>Follow us on</span>
        <a href="#" aria-label="Twitter" class="footer-icon">
          <svg width="28" height="28" fill="#fff" viewBox="0 0 24 24"><path d="M24 4.557a9.93 9.93 0 0 1-2.828.775 4.932 4.932 0 0 0 2.165-2.724c-.951.564-2.005.974-3.127 1.195a4.92 4.92 0 0 0-8.384 4.482C7.691 8.095 4.066 6.13 1.64 3.161c-.542.929-.856 2.01-.857 3.17 0 2.188 1.115 4.116 2.823 5.247a4.904 4.904 0 0 1-2.229-.616c-.054 2.281 1.581 4.415 3.949 4.89a4.936 4.936 0 0 1-2.224.084c.627 1.956 2.444 3.377 4.6 3.417A9.867 9.867 0 0 1 0 21.543a13.94 13.94 0 0 0 7.548 2.209c9.057 0 14.009-7.496 14.009-13.986 0-.21 0-.423-.016-.634A9.936 9.936 0 0 0 24 4.557z"/></svg>
        </a>
        <a href="#" aria-label="YouTube" class="footer-icon">
          <svg width="28" height="28" fill="#fff" viewBox="0 0 24 24"><path d="M23.498 6.186a2.994 2.994 0 0 0-2.107-2.117C19.236 3.5 12 3.5 12 3.5s-7.236 0-9.391.569A2.994 2.994 0 0 0 .502 6.186C0 8.342 0 12 0 12s0 3.658.502 5.814a2.994 2.994 0 0 0 2.107 2.117C4.764 20.5 12 20.5 12 20.5s7.236 0 9.391-.569a2.994 2.994 0 0 0 2.107-2.117C24 15.658 24 12 24 12s0-3.658-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
        </a>
      </div>
    </div>
    <div class="footer-bottom">
      <div class="footer-copyright">
        Copyright © 2022 Amadeus Hotels. All rights reserved.
      </div>
      <div class="footer-credits">
        Photos by
        <a href="https://unsplash.com/@fmooneeram" target="_blank" rel="noopener">Felix Mooneeram</a>
        &amp;
        <a href="https://unsplash.com/@serge_k" target="_blank" rel="noopener">Serge Kutuzov</a>
        on <a href="https://unsplash.com/" target="_blank" rel="noopener">Unsplash</a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: #191919;
  color: #fff;
  width: 100%;
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 1rem;
  letter-spacing: 0.02em;
  margin-top: 0;
}

.footer-main {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  max-width: none;
  width: 100vw;
  margin: 0;
  padding: 32px 180px 24px 180px;
  border-bottom: 2px solid #222;
  box-sizing: border-box;
}

.footer-left {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.footer-title {
  font-weight: 700;
  font-size: 1.15rem;
  margin-bottom: 8px;
  letter-spacing: 0.04em;
}

.footer-address {
  color: #f5f5f5;
  font-size: 1rem;
  line-height: 1.5;
  letter-spacing: 0.04em;
}

.footer-right {
  display: flex;
  align-items: center;
  gap: 18px;
  font-size: 1.1rem;
  color: #fff;
  margin-top: 8px;
}

.footer-icon {
  display: inline-flex;
  align-items: center;
  margin-left: 8px;
  transition: opacity 0.2s;
}
.footer-icon:hover {
  opacity: 0.7;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: none;
  width: 100vw;
  margin: 0;
  padding: 18px 180px 30px 180px;
  background: #191919;
  font-size: 1rem;
  color: #ccc;
  box-sizing: border-box;
}

.footer-copyright {
  color: #ccc;
  font-size: 1rem;
  letter-spacing: 0.03em;
}

.footer-credits {
  color: #ccc;
  font-size: 1rem;
  letter-spacing: 0.03em;
}
.footer-credits a {
  color: #ccc;
  text-decoration: underline;
  margin: 0 2px;
}

@media (max-width: 900px) {
  .footer-main,
  .footer-bottom {
    flex-direction: column;
    align-items: flex-start;
    padding: 24px 24px 16px 24px;
    gap: 12px;
  }
  .footer-right {
    margin-top: 0;
  }
}

/* Mobile  */
@media (max-width: 600px) {
  .footer-main,
  .footer-bottom {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 16px 8px 10px 8px;
    font-size: 0.95rem;
    text-align: center;
    gap: 12px;
  }
  .footer-left {
    align-items: center;
    justify-content: center;
    display: flex;
    flex-direction: column;
    width: 100%;
    text-align: center;
    gap: 4px;
  }
  .footer-right {
    margin-top: 12px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 8px;
    width: 100%;
    text-align: center;
  }
  .footer-title {
    font-size: 1.2rem;
    text-align: center;
  }
  .footer-address {
    text-align: center;
  }
  .footer-icon {
    margin-left: 4px;
    margin-right: 4px;
  }
  .footer-bottom {
    gap: 6px;
  }
  .footer-credits {
    width: 380px;
    text-align: center;
  }
}
</style>