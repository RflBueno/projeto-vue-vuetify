<template>
  <v-app theme="light">
    <v-navigation-drawer v-model="drawerOpen">
      <v-list>
        <v-list-subheader class="d-flex justify-center text-h5">Menu</v-list-subheader>
        <v-list-item prepend-icon="mdi-home">Página Inicial</v-list-item>
        <v-list-item prepend-icon="mdi-account-circle">Usuários</v-list-item>
        <v-list-group value="Configurações">
          <template #activator="{ props }">
            <v-list-item v-bind="props" prepend-icon="mdi-cog" title="Configurações"></v-list-item>
          </template>

          <v-list-item prepend-icon="mdi-translate">Idioma</v-list-item>
          <v-list-item prepend-icon="mdi-help-circle">Suporte</v-list-item>

        </v-list-group>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar class="border-b w-100 elevation-2">
      <v-app-bar-nav-icon @click="drawerOpen = !drawerOpen"></v-app-bar-nav-icon>
      <v-app-bar-tittle class="pl-15 py-2">My App</v-app-bar-tittle>

      <template #append>

        <v-menu>
          <template #activator="{ props }">
            <v-btn v-bind="props" icon class="mr-2">
              <v-badge color="error" content="2">
                <v-icon icon="mdi-bell-outline" size="large"></v-icon>
              </v-badge>
            </v-btn>
          </template>

          <v-card min-width="200px">
            <v-list :lines="false" density="compact">
              <!-- linha 1 card notification -->
              <v-list-item prepend-icon="">
                <v-list-item-title class="notification-truncate">Lorem ipsum dolor sit amet, consectetur adipiscing
                  elit. Sed do
                  eiusmod tempor incididunt ut labore et dolore magna.</v-list-item-title>
              </v-list-item>

              <v-divider></v-divider>

              <!-- linha 2 card notification -->
              <v-list-item prepend-icon="">
                <v-list-item-title class="notification-truncate">Lorem ipsum dolor sit amet, consectetur adipiscing
                  elit. Sed do
                  eiusmod tempor incididunt ut labore et dolore magna.</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-card>
        </v-menu>

        <v-menu>
          <template #activator="{ props }">
            <v-avatar v-bind="props">
              <v-img cover alt="John"
                src="https://preview.redd.it/l0m6jy5zqwxa1.png?width=640&crop=smart&auto=webp&s=c011ad1e3fcf666ade161a3a48ff6419fb944882"></v-img>
            </v-avatar>
          </template>

          <v-card min-width="200px">
            <v-list :lines="false" density="compact">
              <!-- linha 1 card profile -->
              <v-list-item prepend-icon="mdi-account-circle">
                <v-list-item-title>Meu perfil</v-list-item-title>
              </v-list-item>
              <!-- linha 2 card profile -->
              <v-list-item prepend-icon="mdi-shield-account">
                <v-list-item-title>Dados da conta</v-list-item-title>
              </v-list-item>
              <!-- linha 3 card profile -->
              <v-list-item prepend-icon="mdi-heart">
                <v-list-item-title>Itens Salvos</v-list-item-title>
              </v-list-item>
              <!-- linha 4 card profile -->
              <v-list-item prepend-icon="mdi-theme-light-dark">
                <v-list-item-title>Tema</v-list-item-title>
              </v-list-item>
              <!-- linha 5 card profile -->
              <v-list-item prepend-icon="mdi-logout">
                <v-list-item-title>Sair da conta</v-list-item-title>
              </v-list-item>

            </v-list>
          </v-card>

        </v-menu>


      </template>
    </v-app-bar>

    <v-main>
      <v-container>
        <h1 class="d-flex justify-center pl-4">Dashboard</h1>

        <!-- tabela dashboard -->
        <v-card flat class="border mb-8">
          <v-row class="d-flex justify-space-between pt-4 px-3">
            <v-card-title>Últimos usuários</v-card-title>

            <v-card-title>
              <!-- DIALOG OPCAO 1 PRÁTICO MAS MENOS OTIMIZADO EM CASO DE MUITAS LINHAS NA TABLE -->
              <!-- <v-dialog width="500px" max-width="500px">
                <template #activator="{ props }">
                  <v-btn v-bind="props" variant="tonal">
                    Adicionar usuário
                  </v-btn>
                </template>
                <v-card>
                  <v-card-title class="text-h5">Adicionar usuário</v-card-title>
                  <v-card-text>
                    <v-form>
                      <v-text-field label="Nome" variant="outlined"></v-text-field>
                      <v-text-field label="Email" variant="outlined"></v-text-field>
                      <v-btn variant="tonal" color="orange" size="small">Salvar</v-btn>
                    </v-form>
                  </v-card-text>
                </v-card>
              </v-dialog> -->


              <!-- DIALOG OPCAO 2 MELHOR OTIMIZADO EM CASO DE MUITAS LINHAS NA TABLE -->
              <v-btn @click="dialogOpen = true" variant="tonal" size="small">Adicionar usuário</v-btn>
              <v-dialog v-model="dialogOpen" width="600px">
                <v-card>
                  <v-card-title class="d-flex justify-center">Painel de cadastro</v-card-title>
                  <v-card-text>
                    <!-- FORM OPCAO 1 -->
                    <!-- <v-form>
                      <v-text-field clearable label="Nome" variant="outlined"></v-text-field>
                      <v-text-field clearable label="Email" variant="outlined"></v-text-field>
                      <div class="d-flex justify-end mt-2">
                        <v-btn variant="tonal" @click="salvar">
                          Salvar
                        </v-btn>
                      </div>
                    </v-form> -->

                    <v-row>
                      <v-col>
                        <v-text-field label="Nome" variant="outlined"></v-text-field>
                      </v-col>

                      <v-col>
                        <v-text-field label="Email" variant="outlined" :rules="emailRules"></v-text-field>
                      </v-col>
                    </v-row>

                    <v-select label="Cargo" :items="['Admin', 'Gerente', 'Convidado']" variant="outlined"
                      hide-details="true"></v-select>
                  </v-card-text>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn variant="text" @click="dialogOpen = false">Cancelar</v-btn>
                    <v-btn :loading="loading" variant="tonal" @click="load">Salvar</v-btn>
                  </v-card-actions>

                </v-card>
              </v-dialog>
            </v-card-title>
          </v-row>

          <v-table hover>
            <thead>
              <tr>
                <th>ID</th>
                <th>Nome</th>
                <th>Email</th>
                <th>Cargo</th>
                <th>Ações</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>1</td>
                <td>Rafael</td>
                <td>rafael@email.com</td>
                <td>
                  <v-chip>Admin</v-chip>
                </td>
                <td>
                  <v-btn variant="tonal">Editar</v-btn>
                </td>
              </tr>

              <tr>
                <td>2</td>
                <td>Luiz</td>
                <td>luiz@email.com</td>
                <td>
                  <v-chip color="primary">Gerente</v-chip>
                </td>
                <td>
                  <v-btn variant="tonal">Editar</v-btn>
                </td>
              </tr>

              <tr>
                <td>3</td>
                <td>Pedro</td>
                <td>pedro@email.com</td>
                <td>
                  <v-chip color="green">Convidado</v-chip>
                </td>
                <td>
                  <v-btn variant="tonal">Editar</v-btn>
                </td>
              </tr>

            </tbody>
          </v-table>
        </v-card>

        <v-row max-width="100%" class="d-flex justify-center">
          <v-col cols="12" sm="6" md="4" lg="3">
            <!-- CARD 1 -->
            <v-card flat class="card-1 border mx-auto bg-grey-darken-4" max-width="350">
              <v-img class="align-end text-white" :aspect-ratio="4 / 3" cover
                src="https://images.pexels.com/photos/28749416/pexels-photo-28749416/free-photo-of-o-iconico-coliseu-em-roma-ao-anoitecer.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1">
                <v-card-title class="blur-title">10 Curiosidades
                  sobre a Itália</v-card-title>
              </v-img>
              <v-card-subtitle class="mdi mdi-map-marker-radius-outline pt-3">
                Coliseu, Roma
              </v-card-subtitle>
              <v-card-text>
                <div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore
                  et dolore magna.</div>
              </v-card-text>
              <v-card-actions>
                <v-btn prepend-icon="mdi-magnify" variant="tonal" color="orange" size="small" text="Ver mais"></v-btn>
                <v-btn prepend-icon="mdi-share-variant" variant="tonal" color="orange" size="small"
                  text="Compartilhar"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

          <!-- CARD 2 -->
          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="card-2 border mx-auto bg-grey-darken-4" max-width="350">
              <v-img class="align-end text-white" :aspect-ratio="4 / 3" cover
                src="https://images.pexels.com/photos/1562058/pexels-photo-1562058.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1">
                <v-card-title class="blur-title">10 Curiosidades
                  sobre a Noruega</v-card-title>
              </v-img>
              <v-card-subtitle class="mdi mdi-map-marker-radius-outline pt-3">
                Auroras boreais, Tromsø
              </v-card-subtitle>
              <v-card-text>
                <div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore
                  et dolore magna.</div>
              </v-card-text>
              <v-card-actions>
                <v-btn prepend-icon="mdi-magnify" variant="tonal" color="orange" size="small" text="Ver mais"></v-btn>
                <v-btn prepend-icon="mdi-share-variant" variant="tonal" color="orange" size="small"
                  text="Compartilhar"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

          <!-- CARD 3 -->
          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="card-3 border mx-auto bg-grey-darken-4" max-width="350">
              <v-img class="align-end text-white" :aspect-ratio="4 / 3" cover
                src="https://images.pexels.com/photos/248195/pexels-photo-248195.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1">
                <v-card-title class="blur-title">10 Curiosidades
                  sobre o Japão</v-card-title>
              </v-img>
              <v-card-subtitle class="mdi mdi-map-marker-radius-outline pt-3">
                Monte Fuji, Ilha de Honshu
              </v-card-subtitle>
              <v-card-text>
                <div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore
                  et dolore magna.</div>
              </v-card-text>
              <v-card-actions>
                <v-btn prepend-icon="mdi-magnify" variant="tonal" color="orange" size="small" text="Ver mais"></v-btn>
                <v-btn prepend-icon="mdi-share-variant" variant="tonal" color="orange" size="small"
                  text="Compartilhar"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

          <!-- CARD 4 -->
          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="card-4 border mx-auto bg-grey-darken-4" max-width="350">
              <v-img class="align-end text-white" :aspect-ratio="4 / 3" cover
                src="https://images.pexels.com/photos/612451/pexels-photo-612451.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1">
                <v-card-title class="blur-title">10 Curiosidades
                  sobre o Peru</v-card-title>
              </v-img>
              <v-card-subtitle class="mdi mdi-map-marker-radius-outline pt-3">
                Machu Picchu, Cusco
              </v-card-subtitle>
              <v-card-text>
                <div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore
                  et dolore magna.</div>
              </v-card-text>
              <v-card-actions>
                <v-btn prepend-icon="mdi-magnify" variant="tonal" color="orange" size="small" text="Ver mais"></v-btn>
                <v-btn prepend-icon="mdi-share-variant" variant="tonal" color="orange" size="small"
                  text="Compartilhar"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <!-- <HelloWorld /> -->
    </v-main>

    <!-- <AppFooter /> -->
  </v-app>
</template>

<script setup>
import { ref } from 'vue';

const drawerOpen = ref(false);
const dialogOpen = ref(false);
const loading = ref(false);
const emailRules = [
  value => {
    if (value) return true;
    return 'E-mail é obrigatório';
  },
  value => {
    if (value.includes('@')) {
      return true;
    }
    return 'E-mail deve ser válido';
  }
]


// const emailRules = [
//   (v) => !!v || 'E-mail é obrigatório',
//   (v) => /.+@.+\..+/.test(v) || 'E-mail deve ser válido',
// ];

function load() {
  loading.value = true;
  setTimeout(() => {
    loading.value = false;
    dialogOpen.value = false;
  }, 1000);
}

</script>

<style scoped>
.blur-title {
  background-color: rgba(0, 0, 0, 0.2);
  /* escuro semi-transparente */
  backdrop-filter: blur(8px);
  border-radius: 8px;
}

.notification-truncate {
  max-width: 300px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
