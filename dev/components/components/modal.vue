<template>
  <div>
    <div class="layout-padding">
      <p class="caption">
        <span class="desktop-only">Click</span>
        <span class="mobile-only">Tap</span>
        on each type to see it in action.
      </p>

      <div class="list" style="max-width: 600px;">
        <div
          class="item link"
          v-for="modal in types"
          @click="$refs[modal.ref].open()"
        >
          <div class="item-primary">
            <q-icon name="open_in_new" />
          </div>
          <div class="item-content has-secondary">
            <div>{{modal.label}}</div>
          </div>
          <div class="item-secondary">
            <q-icon name="keyboard_arrow_right" />
          </div>
        </div>
      </div>

      <p class="caption">Appear from Edges</p>
      <div class="list" style="max-width: 600px;">
        <div
          class="item link"
          v-for="position in ['top', 'bottom', 'left', 'right']"
          @click="openSpecialPosition(position)"
        >
          <div class="item-primary">
            <q-icon name="open_in_new" />
          </div>
          <div class="item-content has-secondary">
            <div>Modal from {{position}}</div>
          </div>
          <div class="item-secondary">
            <q-icon name="keyboard_arrow_right" />
          </div>
        </div>
      </div>
    </div>

    <q-modal ref="basicModal" :content-css="{padding: '50px', minWidth: '50vw'}">
      <h4>Basic Modal</h4>
      <p v-for="n in 25">Scroll down to close</p>
      <q-btn class="primary" @click="$refs.basicModal.close()">Close</q-btn>
    </q-modal>

    <q-modal
      ref="eventsModal"
      @open="notify('open')"
      @escape-key="notify('escape-key')"
      @close="notify('close')"
      :content-css="{padding: '50px', minWidth: '50vw'}"
    >
      <h4>Modal with Events</h4>
      <p v-for="n in 25">Scroll down to close</p>
      <q-btn class="primary" @click="$refs.eventsModal.close()">Close</q-btn>
    </q-modal>

    <q-modal ref="layoutModal" :content-css="{minWidth: '80vw', minHeight: '80vh'}">
      <q-modal-layout>
        <div slot="header" class="q-toolbar">
          <q-btn @click="$refs.layoutModal.close()">
            <q-icon name="keyboard_arrow_left" />
          </q-btn>
          <div class="q-toolbar-title">
            Header
          </div>
        </div>

        <div slot="header" class="q-toolbar">
          <q-search class="bg-blue-6 auto"></q-search>
        </div>

        <div slot="footer" class="q-toolbar">
          <div class="q-toolbar-title">
            Footer
          </div>
        </div>

        <div class="layout-padding">
          <h1>Modal</h1>

          <q-btn class="primary" @click="$refs.layoutModal.close()">Close</q-btn>
          <p class="caption" v-for="n in 15">This is a Modal presenting a Layout.</p>
        </div>
      </q-modal-layout>
    </q-modal>

    <q-modal ref="minimizedModal" class="minimized" :content-css="{padding: '50px'}">
      <h4>Minimized Modal</h4>
      <p>This one has backdrop on small screens too.</p>
      <q-btn class="red" @click="$refs.minimizedModal.close()">Close Me</q-btn>
    </q-modal>

    <q-modal ref="maximizedModal" class="maximized" :content-css="{padding: '50px'}">
      <h4>Maximized Modal</h4><p>This one is maximized on bigger screens too.</p>
      <q-btn class="tertiary" @click="$refs.maximizedModal.close()">Close Me</q-btn>
    </q-modal>

    <q-modal ref="positionModal" :position="position" :content-css="{padding: '20px'}">
      <h4>Modal</h4><p>This one gets displayed from {{position}}.</p>
      <q-btn class="orange" @click="$refs.positionModal.close()">Close Me</q-btn>
    </q-modal>
  </div>
</template>

<script>
import { Toast } from 'quasar'

export default {
  data () {
    return {
      types: [
        {
          label: 'Basic',
          ref: 'basicModal'
        },
        {
          label: 'Basic with Events',
          ref: 'eventsModal'
        },
        {
          label: 'With Layout',
          ref: 'layoutModal'
        },
        {
          label: 'Always Minimized',
          ref: 'minimizedModal'
        },
        {
          label: 'Always Maximized',
          ref: 'maximizedModal'
        }
      ],
      position: 'bottom'
    }
  },
  methods: {
    notify (eventName) {
      Toast.create(`Event "${eventName}" was triggered.`)
    },
    openSpecialPosition (position) {
      this.position = position
      this.$nextTick(() => {
        this.$refs.positionModal.open()
      })
    }
  }
}
</script>
