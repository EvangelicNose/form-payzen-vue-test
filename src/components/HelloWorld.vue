<template>
  <div class="container">
    <div id="loader" style="color: white;">
      Cargando...
    </div>
    <div id="myPaymentForm" style="display: none;">
      <div class="kr-embedded">
        <!--new flex-container class to indicate a flex-direction: row  -->
        <div class="container">
          <span class="title">
            Nueva tarjeta de crédito
          </span>
          <label>
            Número de tarjeta
          </label>
          <div class="kr-pan"></div>
          <div class="flex-container">
            <div>
              <label>
                Fecha de Expiración
              </label>
              <div class="kr-expiry"></div>
            </div>
            <div>
              <label>
                CVC
              </label>
              <div class="kr-security-code"></div>
            </div>
          </div>
        </div>

        <!-- payment form submit button -->
        <button class="kr-payment-button"></button>
      </div>
    </div>
  </div>
</template>


<script setup>
/* import embedded-form-glue library */
import KRGlue from '@lyracom/embedded-form-glue'
import { ref, onMounted } from 'vue'

let message = ref('')


onMounted(async () => {

  const publicKey = '91335531:testpublickey_lkTl1PQ8E6xM1nAqM28p0RO8BO3Cax8p6ShOQOc5ghQNv'

  const endpoint = 'https://static.payzen.eu/'

  const formToken = "01Av_gi3TUSLmIo6hRiQYbrg245eyJhbW91bnQiOjExMjAwLCJjdXJyZW5jeSI6IkJSTCIsImVxdWl2YWxlbnRWYWx1ZUN1cnJlbmN5IjoiRVVSIiwiZXF1aXZhbGVudFZhbHVlIjoxOTg4LCJtb2RlIjoiVEVTVCIsInZlcnNpb24iOjQsIm9yZGVySWQiOiI4VzQ0RkRZRUY2NiIsInNob3BOYW1lIjoiTHlyYSBTTVMgKFNNUykiLCJmb3JtQWN0aW9uIjoiUkVHSVNURVJfUEFZIiwiYnJhbmRQcmlvcml0eSI6WyJDQiIsIlZJU0EiLCJWSVNBX0RFQklUIiwiVklTQV9FTEVDVFJPTiIsIk1BRVNUUk8iLCJNQVNURVJDQVJEIiwiTUFTVEVSQ0FSRF9ERUJJVCJdLCJjYXRlZ29yaWVzIjp7ImRlYml0Q3JlZGl0Q2FyZHMiOnsiYXBwSWQiOiJjYXJkcyIsInBhcmFtIjpbIkVERU5SRUQiLCJBTUVYIiwiTUFTVEVSQ0FSRF9ERUJJVCIsIlZJU0EiLCJLQURFT1NfQ1VMVFVSRSIsIlZJU0FfREVCSVQiLCJTT0RFWE8iLCJFLUNBUlRFQkxFVUUiLCJDSFFfREVKIiwiTUFTVEVSQ0FSRCIsIlZQQVkiLCJLQURFT1NfR0lGVCIsIlZJU0FfRUxFQ1RST04iLCJBUEVUSVoiLCJDQiJdfX0sImNhcmRzIjp7IkVERU5SRUQiOnsiZmllbGRzIjp7InNlY3VyaXR5Q29kZSI6eyJyZXF1aXJlZCI6ZmFsc2V9fSwiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIkFNRVgiOnsiZmllbGRzIjp7InNlY3VyaXR5Q29kZSI6eyJtYXhMZW5ndGgiOjR9fSwiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIk1BU1RFUkNBUkRfREVCSVQiOnsiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIlZJU0EiOnsiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIktBREVPU19DVUxUVVJFIjp7ImZpZWxkcyI6eyJzZWN1cml0eUNvZGUiOnsicmVxdWlyZWQiOmZhbHNlfX0sImNvcHlGcm9tIjoiY2FyZHMuREVGQVVMVCJ9LCJWSVNBX0RFQklUIjp7ImNvcHlGcm9tIjoiY2FyZHMuREVGQVVMVCJ9LCJTT0RFWE8iOnsiZmllbGRzIjp7InNlY3VyaXR5Q29kZSI6eyJyZXF1aXJlZCI6ZmFsc2V9fSwiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIkUtQ0FSVEVCTEVVRSI6eyJjb3B5RnJvbSI6ImNhcmRzLkRFRkFVTFQifSwiQ0hRX0RFSiI6eyJmaWVsZHMiOnsic2VjdXJpdHlDb2RlIjp7InJlcXVpcmVkIjpmYWxzZX19LCJjb3B5RnJvbSI6ImNhcmRzLkRFRkFVTFQifSwiTUFTVEVSQ0FSRCI6eyJjb3B5RnJvbSI6ImNhcmRzLkRFRkFVTFQifSwiVlBBWSI6eyJmaWVsZHMiOnsic2VjdXJpdHlDb2RlIjp7InJlcXVpcmVkIjpmYWxzZX19LCJjb3B5RnJvbSI6ImNhcmRzLkRFRkFVTFQifSwiS0FERU9TX0dJRlQiOnsiZmllbGRzIjp7InNlY3VyaXR5Q29kZSI6eyJyZXF1aXJlZCI6ZmFsc2V9fSwiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIlZJU0FfRUxFQ1RST04iOnsiZmllbGRzIjp7InNlY3VyaXR5Q29kZSI6eyJyZXF1aXJlZCI6ZmFsc2V9fSwiY29weUZyb20iOiJjYXJkcy5ERUZBVUxUIn0sIkFQRVRJWiI6eyJmaWVsZHMiOnsic2VjdXJpdHlDb2RlIjp7InJlcXVpcmVkIjpmYWxzZX19LCJjb3B5RnJvbSI6ImNhcmRzLkRFRkFVTFQifSwiREVGQVVMVCI6eyJmaWVsZHMiOnsicGFuIjp7Im1pbkxlbmd0aCI6MTAsIm1heExlbmd0aCI6MTksInZhbGlkYXRvcnMiOlsiTlVNRVJJQyIsIkxVSE4iXSwicmVxdWlyZWQiOnRydWUsInNlbnNpdGl2ZSI6dHJ1ZSwiaGlkZGVuIjpmYWxzZSwiY2xlYXJPbkVycm9yIjp0cnVlfSwiZXhwaXJ5RGF0ZSI6eyJyZXF1aXJlZCI6dHJ1ZSwic2Vuc2l0aXZlIjp0cnVlLCJoaWRkZW4iOmZhbHNlLCJjbGVhck9uRXJyb3IiOnRydWV9LCJzZWN1cml0eUNvZGUiOnsibWluTGVuZ3RoIjozLCJtYXhMZW5ndGgiOjQsInZhbGlkYXRvcnMiOlsiTlVNRVJJQyJdLCJyZXF1aXJlZCI6dHJ1ZSwic2Vuc2l0aXZlIjp0cnVlLCJoaWRkZW4iOmZhbHNlLCJjbGVhck9uRXJyb3IiOnRydWV9fX0sIkNCIjp7ImNvcHlGcm9tIjoiY2FyZHMuREVGQVVMVCJ9fSwic21hcnRGb3JtIjp7IkNBUkRTIjp7ImFsbG93SUZyYW1lIjpmYWxzZSwicmFuayI6MCwiZGVhZEVuZFBheW1lbnRNZXRob2QiOmZhbHNlLCJuZXdQYXltZW50UmVxdWlyZWQiOmZhbHNlLCJ3YWxsZXQiOmZhbHNlfX0sInRlc3RDYXJkcyI6WyJEQ0MiXSwiYXBpUmVzdFZlcnNpb24iOiI0LjAiLCJjb3VudHJ5IjoiRlIiLCJqU2Vzc2lvbklkIjoiNWREYkJFOTVDZEYyNTVFMWZlZTdkNTJhYjJjNTJhNkQzMkExRTY4Qi52YWRhcGkwMi10bHMtcHJvZC1mci1seXJhIn00302"

  try {

    const { KR } = await KRGlue.loadLibrary(
      endpoint,
      publicKey
    )

    await KR.button.setLabel("Agregar Tarjeta")

    await KR.setFormConfig({
      // Configuration of formToken
      formToken: formToken,
      // Configuration of placeholders for the payment form non-customizable fields
      "kr-placeholder-expiry": " ",
      "kr-placeholder-security-code": " ",
      "kr-clear-on-error": false,
      // Configuration of the embed form locale
      'kr-language': 'es-CH',
    })

    await KR.renderElements('#myPaymentForm')

    // throw new Error('Error de prueba')


    // Show the payment form only when it's fully loaded, preventing the flickering effect
    await KR.onFormReady(() => {
      document.getElementById('myPaymentForm').style.display = 'flex'
      document.getElementById('loader').style.display = 'none'
    })

    // Handle the form submission

    await KR.validateForm(validatePayment)
    await KR.onSubmit(validatePayment)

  } catch (error) {
    document.getElementById('loader').textContent = 'Error loading the payment form'
    message.value = error + ' (see console for more details)'
  }
})

/* Validate the payment data */
async function validatePayment(paymentData) {
  console.log(paymentData)
  const res = await fetch('http://localhost:3000/validatePayment', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(paymentData)
  })
  if (res.status === 200) message.value = 'Payment successful!'
  return false // Return false to prevent the redirection
}
</script>


<style>
.container {
  display: flex !important;
  flex-direction: column !important;
}

#myPaymentForm {
  justify-content: center;
}

.kr-embedded {
  min-width: 350px;
  margin: 0 !important;
}

.kr-embedded .flex-container {
  flex-direction: row !important;
  width: 100%;
  display: flex;
  gap: 5px;
}

.flex-container>div {
  flex-grow: inherit;
  width: 100%;
}

/* to center the button with the class kr-payment-button */
.kr-embedded .kr-payment-button {
  display: block;
  width: 100%;
}

.kr-custom-input {
  width: 100px;
  height: 100px;
  background-color: red;
  animation-name: example;
  animation-duration: 4s;
}

@font-face {
  font-family: 'SansProRegular';
  src:
    local('SansProRegular'),
    url('./assets/fonts/SourceSansPro-Regular.ttf') format('truetype');
}

@font-face {
  font-family: 'SansProBold';
  src:
    local('SansProBold'),
    url('./assets/fonts/SourceSansPro-Bold.ttf') format('truetype');
}

@font-face {
  font-family: 'SansProSemiBold';
  src:
    local('SansProSemiBold'),
    url('./assets/fonts/SourceSansPro-SemiBold.ttf') format('truetype');
}

</style>