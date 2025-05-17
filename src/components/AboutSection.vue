<template>
  <section id="about">
    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="center">
            <v-col cols="12" md="7">
              <h1 class="font-weight-light display-2">Como funciona?</h1>
              <v-row class="mt-5">
                <v-col cols="12" class="d-flex align-center">
                  <p class="text-justify">
                    O projeto "Tampinha de Bigode" em Marília-SP é uma iniciativa social que arrecada tampinhas plásticas com o objetivo de vendê-las para reciclagem. Os fundos arrecadados são revertidos para a compra de rações, medicamentos, produtos de limpeza, além de contribuir para o cuidado e abrigo de gatos resgatados das ruas. Essa ação não só promove a sustentabilidade através da reciclagem, como também ajuda a cuidar de animais em situação de abandono, promovendo bem-estar e proteção aos gatinhos.
                  </p>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="12" md="5" class="d-none d-md-flex">
              <v-img
                src="@/assets/img/tampinha.png"
                class="d-block ml-auto mr-auto"
                max-width="400px"
              />
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<style scoped>
#about {
  background-color: #f4f7f5;
}
</style>
