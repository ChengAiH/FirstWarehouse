<template>
	<div class="iconed">
		<span class="playpop" :class="{ paused: paused }" v-if="currentMusic && currentMusic.id === songing.id">
			<i></i>
			<i></i>
			<i></i>
		</span>
		<span class="Playiconed" v-else>▶</span>
	</div>
</template>

<script>
	export default {
		props: ["songing","HotbottomSong","paused","currentMusic"]
	}
</script>

<style lang="less">
	.iconed {
		width: 30px;
		height: 30px;

		.Playiconed {
			display: inline-block;
			width: 25px;
			height: 25px;
			padding-left: 7px;
			line-height: 22px;
			border-radius: 50%;
			border: 1px solid #ccc;
			color: #ccc;
			font-size: 14px;
		}

		.playpop {
			display: flex;
			justify-content: space-between;
			align-items: flex-end;

			i {
				width: 6px;
				height: 30px;
				background: red;
				transform-origin: center bottom;

				animation: playre 0.6s linear -0.2s infinite alternate-reverse;

				&:first-of-type {
					animation-delay: 0s;
				}

				&:last-of-type {
					animation-delay: -0.4s;
				}
			}

			&.paused {
				i {
					animation-play-state: paused;
				}
			}
		}
	}
	

	@keyframes playre {
		from {
			transform: scaleY(1);
		}

		to {
			transform: scaleY(0.2);
		}
	}
</style>
