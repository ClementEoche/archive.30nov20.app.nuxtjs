  <template>
  <div class="container">
    <navbar page="home"></navbar>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuesaxLogo from '~/components/VuesaxLogo.vue'
import Navbar from "~/components/navbar";

export default {
  name:"home",
  components: {Navbar}
}
</script>
