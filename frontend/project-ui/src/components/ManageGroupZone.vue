<template>
  <q-card style="min-width: 600px" class="no-border">
    <q-card-section class="flex text-white bg-primary">
      <div class="text-h6">
        Manage Group Zone
      </div>
      <q-space />
      <q-btn flat size="sm" v-close-popup round icon="close" />
    </q-card-section>
    <q-card-section>
      <div class="person-card-flex q-gutter-sm">
        <q-input
          style="margin-bottom: 20px"
          v-model="localGroupZone.groupName"
          dense
          outlined
          required
          label="Name *"
        />
      </div>
    </q-card-section>
    <q-form @submit="confirmSaveGroupZone">
      <div style="min-height: 50px;">
        <q-card-actions align="right">
          <q-btn flat color="primary" label="Cancel" v-close-popup />
          <q-btn label="Save" color="primary" type="submit" />
        </q-card-actions>
      </div>
    </q-form>
  </q-card>
</template>

<script lang="ts">
import Vue from 'vue';
import { GroupZone } from './models';

export default Vue.extend({
  name: 'ManageGroupZone',
  mounted() {
    this.componentReady = true;
    this.localGroupZone = JSON.parse(JSON.stringify(this.groupZone)) as GroupZone;
  },
  data() {
    return {
      localGroupZone: {} as GroupZone,
      componentReady: false
    };
  },
  props: {
    groupZone: {
      type: Object as () => GroupZone
    },
    readOnly: {
      type: Boolean
    }
  },
  methods: {
    confirmSaveGroupZone() {
      this.$emit('save', this.localGroupZone)
    }
  },
  components: {}
});
</script>

<style lang="scss" scoped>
.person-card-flex {
  display: flex;
  flex-wrap: wrap;

  .q-select,
  .q-input,
  .q-toggle,
  div {
    width: 31%;
  }

  .address-input {
    width: 63%
  }
}

.note-label {
  margin-top: 20px;
  color: rgba(0, 0, 0, 0.6);
  font-size: 14px;
}
</style>
