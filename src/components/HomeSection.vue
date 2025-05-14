<template>
  <section id="hero">
    <div>
      <v-img src="@/assets/img/fundodosite.jpg" height="750px"></v-img>

      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="center">
            <v-col cols="12" md="6" xl="8">
              <h1 class="display-2 font-weight-bold mb-4" style="color: black"></h1>
              <h1 class="font-weight-light" style="color: black">
                {{ lebre }}
              </h1>
            </v-col>
            <v-col cols="12" md="6" xl="4" class="hidden-sm-and-down"></v-col>
          </v-row>
        </v-col>
      </v-row>

      <div class="svg-border-waves text-white">
        <v-img src="@/assets/img/borderWaves.svg" />
      </div>
    </div>

    <!-- Seção de cards -->
    <v-container fluid id="features" class="mt-8 mb-8">
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="space-around">
            <v-col
              cols="12"
              sm="4"
              class="text-center"
              v-for="(feature, i) in features"
              :key="i"
            >
              <v-hover v-slot:default="{ hover }">
                <v-card
                  class="card"
                  shaped
                  :elevation="hover ? 10 : 4"
                  :class="{ up: hover }"
                >
                  <v-img
                    :src="feature.img"
                    max-width="100%"
                    class="d-block ml-auto mr-auto"
                    :class="{ 'zoom-efect': hover }"
                  ></v-img>
                  <h1 style="font-size: 35px; color: chocolate">{{ feature.title }}</h1>
                  <h4 class="font-weight-regular subtitle-1">
                    {{ feature.text }}
                  </h4>
                </v-card>
              </v-hover>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>

    <div class="svg-border-waves">
      <img src="~@/assets/img/wave2.svg" />
    </div>

    <!-- Mapa e contador -->
    <v-container fluid class="mt-8 mb-4">
  <v-row class="d-flex align-stretch " style="height: 50vh">
    <!-- Contador -->
    <v-col cols="12" md="6" class="pa-2">
      <v-fade-transition>
        <v-card
  v-if="mostrarCard"
  class="pa-6 fill-height d-flex flex-column justify-space-between align-center"
  style="background: linear-gradient(145deg, #ff9800, #ffa726);"
>
  <!-- Título no topo com ícone maior e colorido -->
  <div class="text-h4 d-flex align-center mb-4" style="color: white;">
    <v-icon
      color="green"
      size="36"
      class="mr-3"
    >mdi-recycle</v-icon>
    Quantidade de tampinhas coletadas até o momento...
  </div>

  <!-- Contador centralizado -->
  <div class="text-h1 font-weight-bold text-center" style="color: white;">
    {{ formatarNumero(contador) }}
    
  </div>

  <!-- Rodapé dos pontos de coleta com animação e ícones -->
  <div
    class="text-center px-4 pb-2"
    style="min-height: 140px; width: 100%; color: white;"
  >
    <v-scale-transition>
      <div v-if="contador === numeroFinal">
        <v-divider class="my-4" style="background-color: white;" />
        <div class="text-h5 mb-2 d-flex align-center justify-center">
  <v-icon size="32" color="blue" class="mr-3">mdi-paw</v-icon>
  Avenida Paulista: 
  <strong class="ml-2 mr-2">{{ formatarNumero(contadorPaulista) }}</strong> tampinhas
</div>
<div class="text-h5 d-flex align-center justify-center">
  <v-icon size="32" color="blue" class="mr-3">mdi-paw</v-icon>
  Parque Ibirapuera: 
  <strong class="ml-2 mr-2">{{ formatarNumero(contadorIbirapuera) }}</strong> tampinhas
</div>

      </div>
    </v-scale-transition>
  </div>
</v-card>






      </v-fade-transition>
    </v-col>

    <!-- Mapa -->
    <v-col  cols="12" md="6" class="pa-2 position-relative" style="position: relative;">
      <div
    style="
      position: absolute;
      top: 16px;
      left: 500px;
      z-index: 10;
      background-color: rgba(255, 255, 255, 0.9);
      padding: 10px 16px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
      opacity: 0.7;
    "
  >
    <v-icon color="orange" class="mr-2">mdi-map-marker</v-icon>
    <span class="text-h6 font-weight-bold" style="color: #333;">Pontos de Coleta</span>
  </div>
      <div id="mapa" class="fill-height rounded" style="width: 100%; z-index: 1;"></div>
    </v-col>
  </v-row>
</v-container>

  </section>
</template>

<script>
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';
import iconUrl from 'leaflet/dist/images/marker-icon.png';
import iconShadow from 'leaflet/dist/images/marker-shadow.png';

export default {
  name: 'MapaLeaflet',
  data() {
    return {
      contador: 0,
      numeroFinal: 10587,
      contadorPaulista: 0,
      contadorIbirapuera: 0,
      mostrarCard: true,
      dialog: false,
      videoId: "i8IvvHJssWE",
      features: [
        {
          img: require("@/assets/img/img1.png"),
          title: "Separe com consciência",
          text: "Separe as tampinhas plásticas e os lacres de latas de forma adequada, evitando contaminar os materiais e garantindo a qualidade das doações..",
        },
        {
          img: require("@/assets/img/img2.png"),
          title: "Verifique os pontos de coleta",
          text: "Verifique os pontos de coleta mais próximos da sua localidade. .",
        },
        {
          img: require("@/assets/img/img3.png"),
          title: "Doe com frequência",
          text: "Contribua com o projeto Tampinhas de Bigode doando suas tampinhas e lacres de latas com frequência. Quanto mais doações forem feitas, maior será o impacto positivo na vida dos animais..",
        },
      ],
    };
  },
  methods: {
  formatarNumero(numero) {
    return new Intl.NumberFormat('pt-BR').format(numero);
  }
},
  mounted() {
    const tempoTotal = 10000; // 10 segundos
    const intervalos = 40;
    const passo = Math.ceil(this.numeroFinal / intervalos);
    const intervaloTempo = tempoTotal / intervalos;

    const intervalo = setInterval(() => {
      this.contador += passo;
      if (this.contador >= this.numeroFinal) {
        this.contador = this.numeroFinal;
        clearInterval(intervalo);
        this.contadorPaulista = 6485;
        this.contadorIbirapuera = 4102;
      }
    }, intervaloTempo);

    delete L.Icon.Default.prototype._getIconUrl;
    L.Icon.Default.mergeOptions({
      iconUrl,
      shadowUrl: iconShadow,
    });

    const mapa = L.map('mapa').setView([-23.55052, -46.633308], 12);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors'
    }).addTo(mapa);

    L.marker([-23.561684, -46.656139])
      .addTo(mapa)
      .bindPopup('Avenida Paulista')
      .openPopup();

    L.marker([-23.587416, -46.657634])
      .addTo(mapa)
      .bindPopup('Parque Ibirapuera');
  }
};
</script>

<style lang="scss">
.circle {
  stroke: white;
  stroke-dasharray: 650;
  stroke-dashoffset: 650;
  -webkit-transition: all 0.5s ease-in-out;
  opacity: 0.3;
}
</style>

<style scoped>
#mapa {
  width: 100%;
  height: 100%;
}

.svg-border-waves .v-image {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 3rem;
  width: 100%;
  overflow: hidden;
}

#hero {
  z-index: 0;
}
.svg-border-waves img {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  margin-bottom: -2px;
  z-index: -1;
}

.card {
  min-height: 500px;
  padding: 10px;
  transition: 0.5s ease-out;
}

.card .v-image {
  margin-bottom: 25px;
  transition: 0.75s;
}

.card h1 {
  margin-bottom: 15px;
}

.zoom-efect {
  transform: scale(1.1);
}

.up {
  transform: translateY(-20px);
  transition: 0.5s ease-out;
}

section {
  position: relative;
}
</style>
