<script>
	import { mapMutations } from 'vuex'
    export default {
        onLaunch: function() {
            console.log('App Launch');
        },
        onShow: function() {
            console.log('App Show')
        },
        onHide: function() {
            console.log('App Hide')
        },
		globalData: {
			test: ''
		},
		methods:{
			...mapMutations(['setUniverifyErrorMsg','setUniverifyLogin'])
		}
    }
</script>

<style lang="scss">
	@import 'uview-ui/index.scss';
    @import './common/uni.css';
</style>
