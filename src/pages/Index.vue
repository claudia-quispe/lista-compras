<template>
  <q-page class="bg-grey-3 column">
    <!-- Lista de Items -->
    <q-list class="bg-white q-pa-md" separator bordered>
      <q-item
        v-for="(item, i) in items"
        :key="i"
        tag="label"
        v-ripple
        clickeable
        :class="{'bg-blue-1 listo': item.listo == true}">
        <q-item-section avatar>
          <q-checkbox v-model="item.listo" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{item.texto}}</q-item-label>
        </q-item-section>
        <q-item-section side>
          <q-btn v-if="item.listo" flat round color="primary" icon="delete" @click.stop="eliminarItem(i)"/>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  name: 'Index',
  data () {
    return {
      items: [
        {
          texto: 'Cloro',
          listo: false
        },
        {
          texto: 'Pan batido',
          listo: false
        },
        {
          texto: 'Chocolate',
          listo: false
        }
      ]
    }
  },
  methods: {
    eliminarItem (i) {
      this.$q.dialog({
        dark: true,
        title: 'Alerta',
        message: 'Estás seguro?'
      }).onOk(() => {
        // esto es cuando el usuario esta ok con el eliminar item
        // eliminamos el tiem
        this.items.splice(i, 1)
        // le notificamos al usuario
        this.$q.notify('El item ha sido eliminado')
      })
    }
  }
}
</script>
