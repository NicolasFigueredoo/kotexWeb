<template>
  <div>
    <div class="indicador">
      <p>Inicio > Catalogo</p>
    </div>
    <div class="catalogo">
      <div class="informacionCatalogo">
        <img id="imgCatalogo" src="../../img/catalogo.jpg" alt="">
      </div>
      <div class="catalogoBotones">
        <p class="catalogoTitle">Catálogo de productos</p>
        <div class="catalogoText">
          <p>Descargá nuestro catálogo actualizado con todos nuestros artículos en venta</p>
        </div>
        <div class="botones">
          <button @click="descargarArchivo()" type="button" id="descargar" class="btn"
            style="width: 184px; height: 50px;">Descargar</button>
          <a href="/api/obtenerCatalogo" target="_blank">
            <button type="button" id="visualizar" class="btn" style="width: 184px; height: 50px;">Visualizar</button>
          </a>
        </div>

      </div>

    </div>


  </div>

</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      catalogo: null,
      link: null
    }
  },

  methods: {
    descargarArchivo() {
      axios.get('/api/obtenerCatalogo',{ responseType: 'blob' })
        .then(response => {
          const url = window.URL.createObjectURL(new Blob([response.data]));
          const link = document.createElement('a');
          this.link = url;
          link.href = url;
          link.setAttribute('download', 'catalogo.pdf');
          document.body.appendChild(link);
          link.click();

        })
        .catch(error => {
          console.error(error);
        });
    },
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

#descargar {
  background-color: #2F3F78;
  color: white;
  border-radius: 0%;
}

#visualizar {
  background-color: white;
  color: black;
  border-radius: 0%;
  margin-left: 20px;

}

.catalogoTitle {
  font-weight: 600;
  font-family: "Montserrat", sans-serif;
  font-size: 24px;

}

.catalogoText {
  font-weight: 400;
  font-family: "Montserrat", sans-serif;
  font-size: 16px;
}

.catalogoBotones {
  display: flex;
  flex-direction: column;
  padding: 70px;
  font-weight: 400;
  font-family: "Montserrat", sans-serif;
  font-size: 13px;
  width: 100%;
}

.botones {
  display: flex;
  justify-content: start;
}

.indicador {
  color: black;
  margin-top: 10px;
  margin-left: 17%;
  font-size: 15px;
  font-weight: 500;
  font-family: "Montserrat", sans-serif;
  line-height: 60px;
}

.catalogo {
  background-color: #FAFAFA;
  height: 420px;
  display: flex;
  justify-content: center;
  margin-left: 32%;
  margin-right: auto;
  width: 40%;
  margin-bottom: 100px;


}

.informacionCatalogo {
  display: flex;
  justify-content: start;
}

#imgCatalogo {
  width: 320px;
  height: 420px;
}


@media only screen and  (max-width: 1800px) {

  .catalogo {
    width: 60%;
  }

  .catalogoBotones{
    width: 400px;

  }

  .catalogoTitle{
    font-size: 20px;
  }

 }

 @media only screen and  (max-width: 1200px) {

.catalogo {
  width: 65%;
  margin-left: 20%;

}

.catalogoBotones{
  width: 400px;

}

.catalogoTitle{
  font-size: 20px;
}

}

@media only screen and  (max-width: 800px) {
  .catalogo {
    width: 48%;
    margin-top: 200px;
  display: flex;
  flex-direction: column

}
.catalogoBotones{
  padding: 50px;
}
}

@media only screen and  (max-width: 500px) {
  .catalogo {
    width: 60%;
    margin-bottom: 200px;

}

.catalogoBotones{
  width: 100%;
  padding: 0px;
}


.catalogoTitle{
  font-size: 15px;
}
.catalogoText{
  font-size: 15px;
  width: 150px;
}
.informacionCatalogo{
  width: 100%
}
#imgCatalogo{
  width: 100%
}

.botones{
  display: flex;
  flex-direction: column
}
}
</style>
