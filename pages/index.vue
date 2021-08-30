<template>

  <div>
    <!--Основной блок-->
  <v-card
    max-width="600"
    class="mx-auto"
  >
    <v-toolbar
      dark
    >
      <v-btn
        small
        class="ma-2"
        outlined
        fab
        color="teal"
      >
        <v-icon @click="addItem">mdi-plus</v-icon>
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon @click="dialog = true">mdi-information</v-icon>
      </v-btn>
    </v-toolbar>

    <v-list
      subheader
      two-line
    >

      <v-list-item
        v-for="(folder, index) in folders"
        :key="folder.title"
      >
        <v-list-item-avatar>
          <v-icon
            class="grey lighten-1"
            dark
          >
            mdi-folder
          </v-icon>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title v-text="folder.title"></v-list-item-title>

          <v-list-item-subtitle v-text="folder.subtitle"></v-list-item-subtitle>
        </v-list-item-content>

        <v-list-item-action>
          <v-btn icon>
            <v-icon color="red lighten-1" @click="deleteElement(index)">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
      </v-list-item>

    </v-list>
  </v-card>
    <!--Модальное окно-->
  <v-dialog
    v-model="dialog"
    max-width="500px"
  >
    <v-card>
      <v-card-title>
        <span>Количество элементов: {{countFix}}</span>
        <v-spacer></v-spacer>

            <v-btn
              icon
              left
              @click="dialog = false"
            >
              <v-icon>mdi-close</v-icon>
            </v-btn>


      </v-card-title>
    </v-card>
  </v-dialog>
  </div>
</template>

<script>
  export default {
    data: () => ({
      folders: [
        {
          subtitle: 'text',
          title: 'Title user #1',
        },
        {
          subtitle: 'text',
          title: 'Title user #2',
        },
        {
          subtitle: 'text',
          title: 'Title user # 3',
        },
      ],
      dialog: false,
      countFix: '',
      count: ''
    }),
    created: function () {
      this.fCount();
    },
    methods: {
      // Добавление элементов
      addItem() {
        this.folders.push({
          subtitle: 'text',
          title: 'Title user #'+this.count,
        });
        this.count = this.count+1;
        this.countFix = this.countFix+1;
      },
      // Подсчёт количества элементов (мат.сонова+-)
      fCount() {
        this.count = this.folders.length+1;
        this.countFix = this.folders.length;
      },
      // Удаление элементов
      deleteElement: function(index) {
        this.folders.splice(index, 1);
        this.countFix = this.countFix-1;
      }
    },
  }
</script>

