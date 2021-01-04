<template>
	<div class="play-full-footer">
		<div class="play-full-footer-icon">
		</div>
		<div class="progresstime">
			<div class="progressleft"><span class="spanleft">{{currentTime | currentTimeprogress}}</span></div>
			<div class="progress">
				<input type="range" min="0" :max="duration" step="1" @input="getValue" :value="currentTime" />
				<span class="progressmiddle" :style="{ width: (currentTime / duration) * 100 + '%' }"></span>
			</div>
			<div class="progressright"><span class="spanright">{{duration | durationprogress}}</span></div>
		</div>
		<div class="Playplatoon">
			<div class="Play">
				<div class="Playright" @click="poplast">
					<svg height="50" width="50">
						<polygon points="18,26 38,11 38,38" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
						<line x1="18" y1="13" x2="18" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
				<div class="Playmiddle" @click="pop">
					<svg height="50" width="50" v-if="paused">
						<polygon points="38,26 18,13 18,36" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
					</svg>
					<svg height="50" width="50" v-else>
						<line x1="18" y1="13" x2="18" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
						<line x1="30" y1="13" x2="30" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
				<div class="Playleft" @click="popnext">
					<svg height="50" width="50">
						<polygon points="38,26 18,13 18,36" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
						<line x1="38" y1="13" x2="38" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: ["currentTime", "duration","playlist","PlayNext","isShowPlayBar","isShowLyric","paused"],
		data: function() {
			return {};
		},
		filters: {
			durationprogress: function(value) {
				var minute;
				minute = Math.floor(value / 60);
				value = Math.floor(value % 60);
				return minute + ":" + value
			},
			currentTimeprogress: function(value) {
				var minute;
				minute = Math.floor(value / 60);
				value = Math.floor(value % 60);
				return minute + ":" + value
			}
		},
		methods: {
			getValue: function(e) {
				this.$emit("update:currentTime", e.target.value);
			},
			pop:function(){
				this.$emit('togglePlayState')
			},
			popnext:function(){
				this.$emit('PlayNext')
			},
			poplast:function(){
				this.$emit('PlayLast')
			},
		},
	};
</script>

<style lang="less">
	.play-full-footer {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;

		.play-full-footer-icon {
			width: 50px;
			height: 50px;
			position: relative;
			display: flex;

			svg {
				path {
					color: #fff;
				}
			}

			.icon_collection {
				width: 50px;
				height: 40px;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 4.375rem;
			}

			.icon_download {
				width: 50px;
				height: 40px;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 8.75rem;
			}

			.icon_new {
				width: 50px;
				height: 40px;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 13.125rem;
			}

			.icon_information {
				width: 50px;
				height: 50px;
				border-radius: 50%;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 17.5rem;

				svg {
					width: 50px;
					height: 50px;
					border-radius: 50%;
				}
			}

			.icon_list {
				width: 50px;
				height: 50px;
				border-radius: 50%;
				flex: 1 1 auto;
				margin-left: 21.875rem;

				svg {
					width: 50px;
					height: 50px;
				}
			}
		}

		.progresstime {
			display: flex;
			margin-top: 15px;

			.progressleft {
				width: 20%;
				height: 20px;
				font-size: 10px;
				color: #c0c0c0;
				flex: 2 1 auto;

				span {
					padding-left: 40px;
				}
			}

			.progress {
				width: 60%;
				height: 1px;
				background: linear-gradient(to right, lightblue, lightcoral);
				position: relative;
				top: 6px;
				left: 0;
				margin: 0 auto;
				border-radius: 3px;
				flex: 1 1 auto;

				input {
					width: 100%;
					position: absolute;
					top: 0;
					left: 0;
					z-index: 99;
					opacity: 0;
				}

				.progressmiddle {
					display: block;
					position: absolute;
					top: 0;
					left: 0;
					width: 0%;
					height: 100%;
					border-radius: 3px;
				}
			}

			.progressright {
				width: 20%;
				height: 20px;
				font-size: 10px;
				color: #c0c0c0;
				flex: 1 1 auto;

				span {
					padding-left: 20px;
				}
			}
		}

		.Playplatoon {
			width: 100%;
			height: 100px;

			.Play {
				display: flex;
				margin-top: 5%;
				.Playleft {
					width: 50px;
					height: 50px;
					border-radius: 50%;
					margin-left: 10%;
					z-index: 5;
				}

				.Playmiddle {
					width: 50px;
					height: 50px;
					border: 1px solid #FFF;
					border-radius: 50%;
					margin-left: 10%;
					z-index: 5;
				}

				.Playright {
					width: 50px;
					height: 50px;
					border-radius: 50%;
					margin-left: 20%;
					z-index: 5;
				}
			}

		}
	}
</style>
