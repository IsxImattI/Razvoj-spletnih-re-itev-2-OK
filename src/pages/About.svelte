<script>
  let company = {
    name: "Izposojevalnica družabnih iger",
    description:
      "Ponujamo širok izbor družabnih iger za vse starosti in okuse. Naše poslanstvo je, da povežemo ljudi preko igre in zabave.",
    contact: {
      email: "kontakt@izposojevalnica-iger.si",
      phone: "+386 41 123 456",
      address: "Cesta družabnih iger 10, 1000 Ljubljana, Slovenija",
    },
    vision: "Naša vizija je ustvariti skupnost, kjer igre povezujejo družine, prijatelje in znance.",
  };
</script>

<div class="about-container">
  <div class="about">
    <h3 class="about-title">{company.name}</h3>
    <p class="about-description">{company.description}</p>
    <div class="about-info">
      <h4>Kontaktne informacije:</h4>
      <ul>
        <li><strong>Email:</strong> {company.contact.email}</li>
        <li><strong>Telefon:</strong> {company.contact.phone}</li>
        <li><strong>Naslov:</strong> {company.contact.address}</li>
      </ul>
    </div>
    <div class="about-vision">
      <h4>Naša vizija:</h4>
      <p>{company.vision}</p>
    </div>
  </div>
</div>

<style>
.about-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 14rem auto; /* Zmanjšamo zgornji in spodnji rob */
}

.about {
  background-color: #f8f9fa;
  padding: 8rem;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  margin-top: -14rem; /* Dodamo samo malo razmika od naslova */
}

.about-title {
  color: #007bff;
  font-weight: bold;
  margin-bottom: 1rem;
}

.about-description {
  margin-bottom: 1.5rem;
  color: #333;
  line-height: 1.6;
}

.about-info,
.about-vision {
  margin-top: 1rem;
}

ul {
  list-style: none;
  padding: 0;
  text-align: left;
}

ul li {
  margin: 0.5rem 0;
}

strong {
  color: #007bff;
}

@media (max-width: 480px) {
  .about {
    padding: 1rem;
  }

  .about-title {
    font-size: 1.2rem;
  }

  .about-description {
    font-size: 0.9rem;
  }
}


</style>
