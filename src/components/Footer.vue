<template>
    <!-- footer -->
	<v-footer
		dark
		height="auto"
	>
		<v-layout>
			<v-flex xs12>
				<v-card
					flat
					tile
					class="darken-1 white--text text-xs-center"
					width="100vw"
					color="#248ea9"
				>
					<v-card-text>
						
						<v-layout xs12 align-center row>
							<v-flex xs4>
								<v-menu open-on-hover top offset-y>
									<v-btn slot="activator" color="#404969">TODAY: {{todayView}}</v-btn>
									<v-card class="visit-card" 
											color="rgba(184,193,204, 0.7)" 
											width="200px">
										<v-card-title class="title font-weight-light justify-center pb-0">TODAY</v-card-title>
										<v-card-text class="headline font-weight-bold">{{todayView}}</v-card-text>
										<v-card-title class="title font-weight-light justify-center py-0">TOTAL</v-card-title>
										<v-card-text class="headline font-weight-bold">{{totalView}}</v-card-text>				
									</v-card>
								</v-menu>
							</v-flex>
							<v-flex xs4> 
								<v-btn
									v-for="ii in icons"
									:key="ii.emoji"
									:href='ii.link'
									class="mx-3 white--text footer-icons"
									icon
								>
									<v-icon size="24px">{{ ii.emoji }}</v-icon>
								</v-btn>
								<p class="white--text my-1">Please contact us if you have any question. </p>
							</v-flex>
							<v-flex xs4>
								<v-menu open-on-hover top offset-y>
									<template slot="activator">
										<v-avatar size="45px"><img :src="iconURL" alt="weather__avatar" style="backgroundColor:#f4f6f6;"></v-avatar>
										<span class="ml-2">{{ description }}, {{currentTemp}} &deg;</span>
									</template>
									<Weather />
								</v-menu>
							</v-flex>
						</v-layout>
						
					</v-card-text>


					<v-divider></v-divider>

					<v-card-text class="white--text">
						&copy;2019 — <strong>TEN</strong>
					</v-card-text>
				</v-card>
			</v-flex>
		</v-layout>
		
	</v-footer>
	<!-- end footer -->
</template>

<script>
import WeatherApi from '../services/WeatherApi'
import Weather from '../components/Weather'
import FirebaseService from '../services/FirebaseService'

export default {
	name: 'Footer',
	data() {
		return {
			icons: [
				{ emoji:'fa-facebook', link: 'https://www.facebook.com/hellossafy/'},
				{ emoji:'fa-instagram', link: 'https://www.instagram.com/hellossafy/'},
				{ emoji: 'fa-gitlab', link: 'https://lab.ssafy.com/metleeha/webmobile-sub2' }
			],
			iconURL: '',
			currentTemp: '',
			description: '',
			todayView: 0,
			totalView: 0
		}
	},
	components: {
		Weather
	},
	methods:{
		async initViewLog() {
			this.todayView = await FirebaseService.getTodayView()
			this.totalView = await FirebaseService.getTotalView()
			this.totalView += this.todayView
		}
	},
	created() {
		this.initViewLog()

		const weatherData = WeatherApi.loadCoords()        
        .then(data => {
			this.iconURL = "http://openweathermap.org/img/w/" + data.weather[0].icon+ ".png";
			this.description = data.weather[0].description;
			this.currentTemp = Math.round(data.main.temp);
			this.description = data.weather[0].description;
		})
		
	}
}
</script>
<style scoped>
.visit-card{
	text-align: center;
}
.footer-icons {
	display: inline-flex;
}
</style>
