<template>
  <ScaleBox />
</template>

<script lang="ts">
import { Component, Vue, Watch, Ref} from 'vue-property-decorator'
import ScaleBox from './scalebox.vue'

@Component({name: 'Databoard', components: {ScaleBox}})
export default class extends Vue{

}
</script>