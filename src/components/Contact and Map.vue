<template>
  <section class="contact-section">
    <div class="contact-container">
      <div class="contact-form-area">
        <h2>How to reach us</h2>
        <p>Lorem ipsum dolor sit amet, consetetur.</p>
        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-row">
            <div class="form-group">
              <label for="firstName">First Name *</label>
              <input
                id="firstName"
                type="text"
                v-model="form.firstName"
                :class="{ error: errors.firstName }"
                required
              />
              <div v-if="errors.firstName" class="error-message">{{ errors.firstName }}</div>
            </div>
            <div class="form-group">
              <label for="lastName">Last Name *</label>
              <input
                id="lastName"
                type="text"
                v-model="form.lastName"
                :class="{ error: errors.lastName }"
                required
              />
              <div v-if="errors.lastName" class="error-message">{{ errors.lastName }}</div>
            </div>
          </div>
          <div class="form-group">
            <label for="email">Email *</label>
            <input
              id="email"
              type="email"
              v-model="form.email"
              :class="{ error: errors.email }"
              required
            />
            <div v-if="errors.email" class="error-message">{{ errors.email }}</div>
          </div>
          <div class="form-group">
            <label for="telephone">Telephone</label>
            <input
              id="telephone"
              type="tel"
              v-model="form.telephone"
            />
          </div>
          <div class="form-group">
            <label for="message">Message *</label>
            <textarea
              id="message"
              rows="4"
              v-model="form.message"
              :class="{ error: errors.message }"
              required
            ></textarea>
            <div v-if="errors.message" class="error-message">{{ errors.message }}</div>
          </div>
          <div class="form-note">* required fields</div>
          <div class="form-row form-checkbox-row">
            <input
              id="terms"
              type="checkbox"
              v-model="form.terms"
              :class="{ error: errors.terms }"
              required
            />
            <label for="terms">
              I agree to the <a href="#">Terms & Conditions</a>
            </label>
          </div>
          <div v-if="errors.terms" class="error-message">{{ errors.terms }}</div>
          <button type="submit" class="submit-btn">SUBMIT</button>
        </form>
      </div>
      <div class="contact-map-area">
        <iframe
          title="map"
          src="https://www.google.com/maps?q=C.+Salvador+de+Madariaga,+1,+28027+Madrid,+Spain&output=embed"
          style="border:0;"
          allowfullscreen
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
        ></iframe>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive } from 'vue';

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  telephone: '',
  message: '',
  terms: false,
});

const errors = reactive({
  firstName: '',
  lastName: '',
  email: '',
  message: '',
  terms: '',
});

function validateEmail(email) {
  // Simple email regex
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

function handleSubmit() {
  // Reset errors
  errors.firstName = '';
  errors.lastName = '';
  errors.email = '';
  errors.message = '';
  errors.terms = '';

  let valid = true;

  if (!form.firstName.trim()) {
    errors.firstName = 'First name is required';
    valid = false;
  }
  if (!form.lastName.trim()) {
    errors.lastName = 'Last name is required';
    valid = false;
  }
  if (!form.email.trim()) {
    errors.email = 'Email is required';
    valid = false;
  } else if (!validateEmail(form.email)) {
    errors.email = 'Enter a valid email address';
    valid = false;
  }
  if (!form.message.trim()) {
    errors.message = 'Message is required';
    valid = false;
  }
  if (!form.terms) {
    errors.terms = 'You must agree to the Terms & Conditions';
    valid = false;
  }

  if (valid) {
    alert(
      `First Name: ${form.firstName}\nLast Name: ${form.lastName}\nEmail: ${form.email}\nTelephone: ${form.telephone}\nMessage: ${form.message}\nAgreed to Terms: ${form.terms ? 'Yes' : 'No'}`
    );
    // Optionally reset form here
  }
}
</script>

<style scoped>
.contact-section {
  background: #111;
  color: #fff;
  font-family: 'Montserrat', Arial, sans-serif;
  width: 100%;
  min-height: 100vh;
  padding: 52px;
}

.contact-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-start;
  max-width: 1536px;
  margin: 0 auto;
  padding: 48px 32px 0 32px;
  gap: 100px;
}

.contact-form-area {
  max-width: 580px;
}

.contact-form-area h2 {
  font-size: 2rem;
  letter-spacing: 0.08em;
  font-weight: 600;
  margin-bottom: 12px;
}

.contact-form-area p {
  color: #ccc;
  font-size: 1.1rem;
  margin-bottom: 32px;
  letter-spacing: 0.03em;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.form-row {
  display: flex;
  gap: 18px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 1rem;
  margin-bottom: 6px;
  color: #fff;
  letter-spacing: 0.02em;
}

.form-group input,
.form-group textarea {
  background: #2d2c2b;
  border: none;
  color: #fff;
  padding: 10px 12px;
  font-size: 1rem;
  margin-bottom: 0;
  resize: none;
  border: 2px solid transparent;
  transition: border 0.2s;
}

.form-group input.error,
.form-group textarea.error,
.form-checkbox-row input.error {
  border: 2px solid #ff4444;
}

.form-group textarea {
  min-height: 80px;
  max-width: 100%;
}

.error-message {
  color: #ff4444;
  font-size: 0.95rem;
  margin-top: 4px;
  margin-bottom: -8px;
}

.form-note {
  font-size: 0.95rem;
  color: #ccc;
  margin-top: -8px;
  margin-bottom: 0;
}

.form-checkbox-row {
  align-items: center;
  gap: 10px;
  margin-bottom: 0;
}

.form-checkbox-row input[type="checkbox"] {
  width: 20px;
  height: 20px;
  accent-color: #ffc300;
  margin-right: 8px;
  border: 2px solid transparent;
  transition: border 0.2s;
}

.form-checkbox-row input.error {
  border: 2px solid #ff4444;
}

.form-checkbox-row label {
  font-size: 1rem;
  color: #fff;
  cursor: pointer;
}

.form-checkbox-row a {
  color: #fff;
  text-decoration: underline;
}

.submit-btn {
  background: #ffc300;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 12px 0;
  font-size: 1.1rem;
  font-family: inherit;
  font-weight: 500;
  margin-top: 10px;
  width: 180px;
  align-self: flex-end;
  cursor: pointer;
  transition: background 0.2s;
}
.submit-btn:hover {
  background: #e6b100;
}

.contact-map-area {
  width: 100%;
  max-width: 1536px;
  min-width: 320px;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  position: relative;
  bottom: 0px;
  margin-top: 130px;
}

.contact-map-area iframe {
  width: 100%;
  height: 550px;
  border: none;
  border-radius: 0;
  min-width: 260px;
  bottom: 0;
  margin-bottom: 0;
}

@media (max-width: 1024px) {
  .contact-container {
    flex-direction: column;
    gap: 32px;
    padding: 32px 8px 0 8px;
    max-width: 700px;
  }
  .contact-form-area,
  .contact-map-area {
    max-width: 100%;
    width: 100%;
  }
  .contact-map-area iframe {
    height: 300px;
  }
  .submit-btn {
    width: 100%;
    align-self: stretch;
  }
}

/* Mobile  */
@media (max-width: 600px) {
  .contact-section {
    padding: 0 30px;
  }
  .contact-container {
    flex-direction: column;
    gap: 24px;
    padding: 18px 2vw 0 2vw;
    max-width: 100vw;
  }
  .contact-container > * {
    margin-top: 30px;
  }
  .contact-form-area h2 {
    font-size: 1.5rem;
  }
  .contact-form-area p {
    font-size: 0.95rem;
    margin-bottom: 18px;
  }
  .form-row {
    flex-direction: column;
    gap: 0;
  }
  .form-checkbox-row {
    flex-direction: row !important;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .form-checkbox-row label,
  .form-checkbox-row a {
    font-size: 0.8rem;
    white-space: normal;
  }
  .form-checkbox-row input[type="checkbox"] {
    width: 16px;
    height: 16px;
  }
  .contact-map-area iframe {
    height: 180px;
  }

  .submit-btn{
    padding: 12px 0;
    width: 150px;
    align-self: center;
  }
  .contact-map-area {
    width: 100vw;
    max-width: 100vw;
    min-width: 100vw;
    margin-left: -38px;
  }

  .contact-map-area iframe {
    width: 100vw;
    min-width: 100vw;
    height: 450px;
    display: block;
  }
}
</style>