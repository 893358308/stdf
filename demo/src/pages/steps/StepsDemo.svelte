<!--Steps Demo -->
<script>
	import { Steps, Button, Divider } from 'stdf';
	import injCom1 from './injCom1.svelte';
	import injCom2 from './injCom2.svelte';

	const steps = [
		{ step: { title: '起床' } },
		{ step: { title: '吃饭' } },
		{ step: { title: '喝水' } },
		{ step: { title: '打豆豆' } },
		{ step: { title: '睡觉' } },
	];
	const steps1 = [
		{ step: { title: '起床', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-line' } } } },
		{ step: { title: '吃饭', bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } } } },
		{ step: { title: '喝水', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } } },
		{ step: { title: '打豆豆', bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } } } },
		{ step: { title: '睡觉', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } } },
	];
	const steps2 = [
		{ step: { title: '起床' }, finishStep: { title: '已起床' } },
		{ step: { title: '吃饭' }, finishStep: { title: '吃饱了' } },
		{ step: { title: '喝水' }, finishStep: { title: '喝足了' } },
		{ step: { title: '打豆豆' }, finishStep: { title: '打爽了' } },
		{ step: { title: '睡觉' }, finishStep: { title: '睡着了' } },
	];
	const steps3 = [
		{
			step: { title: '起床', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-line' } } },
			finishStep: { title: '已起床', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-fill' } } },
		},
		{
			step: { title: '吃饭', bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } } },
			finishStep: { title: '吃饱了', bar: { type: 'icon', icon: { name: 'ri-restaurant-2-fill' } } },
		},
		{
			step: { title: '喝水', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } },
			finishStep: { title: '喝足了', bar: { type: 'icon', icon: { name: 'ri-cup-fill' } } },
		},
		{
			step: { title: '打豆豆', bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } } },
			finishStep: { title: '打爽了', bar: { type: 'icon', icon: { name: 'ri-emotion-sad-fill' } } },
		},
		{
			step: { title: '睡觉', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } },
			finishStep: { title: '睡着了', bar: { type: 'icon', icon: { name: 'ri-zzz-fill' } } },
		},
	];
	const steps4 = [
		{ step: { title: '起床', desc: '起床搬砖了！' } },
		{ step: { title: '吃饭', desc: '吃吃吃，肥死你。' } },
		{ step: { title: '喝水', desc: '慢慢走路，多多喝水。' } },
		{
			step: {
				title: '打豆豆',
				desc: '吃饭睡觉，打豆豆很爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽。顺便验证进度条高度自适应步骤文字高度。',
			},
		},
		{ step: { title: '睡觉', desc: '吃太饱，睡不着。' } },
	];
	const steps5 = [
		{ step: { title: '起床', desc: '起床搬砖了！', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-line' } } } },
		{
			step: {
				title: '吃饭',
				desc: '吃吃吃，肥死你。',
				bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } },
			},
		},
		{ step: { title: '喝水', desc: '慢慢走路，多多喝水。', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } } },
		{
			step: {
				title: '打豆豆',
				desc: '吃饭睡觉，打豆豆很爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽爽。顺便验证进度条高度自适应步骤文字高度。',
				bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } },
			},
		},
		{ step: { title: '睡觉', desc: '吃太饱，睡不着。', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } } },
	];
	const steps6 = [
		{
			step: { title: '起床', desc: '起床搬砖了！', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-line' } } },
			finishStep: {
				title: '已起床',
				desc: '砖已经搬完了！',
				bar: { type: 'icon', icon: { name: 'ri-hotel-bed-fill' } },
			},
		},
		{
			step: {
				title: '吃饭',
				desc: '吃吃吃，肥死你。',
				bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } },
			},
			finishStep: {
				title: '吃饱了',
				desc: '饭已经全部被吃完了！',
				bar: { type: 'icon', icon: { name: 'ri-restaurant-2-fill' } },
			},
		},
		{
			step: { title: '喝水', desc: '慢慢走路，多多喝水。', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } },
			finishStep: {
				title: '喝足了',
				desc: '水喝太多，从眼睛里溢出来了！',
				bar: { type: 'icon', icon: { name: 'ri-cup-fill' } },
			},
		},
		{
			step: {
				title: '打豆豆',
				desc: '吃饭睡觉，打豆豆。',
				bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } },
			},
			finishStep: {
				title: '打爽了',
				desc: '豆豆已经被打趴下了。',
				bar: { type: 'icon', icon: { name: 'ri-emotion-sad-fill' } },
			},
		},
		{
			step: { title: '睡觉', desc: '吃太饱，睡不着。', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } },
			finishStep: {
				title: '睡着了',
				desc: '睡着了正在做梦呢！',
				bar: { type: 'icon', icon: { name: 'ri-zzz-fill' } },
			},
		},
	];
	const steps7 = [
		{ step: { title: '起床', desc: '起床搬砖了！', bar: '1' } },
		{ step: { title: '吃饭', desc: '吃吃吃，肥死你。', bar: '吃' } },
		{ step: { title: '喝水', desc: '慢慢走路，多多喝水。', bar: '3' } },
		{
			step: {
				title: '打豆豆',
				desc: '吃饭睡觉，打豆豆。',
				bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } },
			},
		},
		{ step: { title: '睡觉', desc: '吃太饱，睡不着。', bar: '😴' } },
	];
	const steps8 = [
		{ step: { title: '起床', bar: { type: 'image', image: './assets/images/avatar_2.png' } } },
		{ step: { title: '吃饭', bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } } } },
		{ step: { title: '喝水', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } } },
		{ step: { title: '打豆豆', bar: { type: 'image', image: './assets/images/avatar_1.jpg' } } },
		{ step: { title: '睡觉', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } } },
	];
	const steps9 = [
		{ step: { title: '起床', desc: '起床搬砖了！', bar: { type: 'icon', icon: { name: 'ri-hotel-bed-line' } } } },
		{
			step: {
				title: '吃饭',
				desc: '吃吃吃，肥死你。',
				bar: { type: 'icon', icon: { name: 'ri-restaurant-2-line' } },
				injComponent: injCom1,
			},
		},
		{ step: { title: '喝水', desc: '慢慢走路，多多喝水。', bar: { type: 'icon', icon: { name: 'ri-cup-line' } } } },
		{
			step: {
				title: '打豆豆',
				desc: '吃饭睡觉，打豆豆。',
				bar: { type: 'icon', icon: { name: 'ri-emotion-sad-line' } },
				injComponent: injCom2,
			},
		},
		{ step: { title: '睡觉', desc: '吃太饱，睡不着。', bar: { type: 'icon', icon: { name: 'ri-zzz-line' } } } },
	];

	let current = 1;
	const preFun = () => {
		current > 1 && current--;
	};
	const nextFun = () => {
		current < steps.length + 1 && current++;
	};
</script>

<div class="mt-8 px-4 mb-4 font-bold text-2xl">横向排列</div>
<div class="mt-8 px-4 mb-4 font-bold text-lg">简单用法</div>
<Steps {steps} {current} />

<div class="mt-8 px-4 mb-4 font-bold text-lg">不同圆角</div>
<Steps {steps} {current} radius="none" />
<Steps {steps} {current} radius="full" />

<div class="mt-8 px-4 mb-4 font-bold text-lg">带图标</div>
<Steps steps={steps1} {current} />

<div class="mt-8 px-4 mb-4 font-bold text-lg">图标不同边框</div>
<Steps steps={steps1} {current} barBorder={false} />
<Steps steps={steps1} {current} barBorder={false} radius="full" />
<Steps steps={steps1} {current} radius="none" />
<Steps steps={steps1} {current} radius="xl" />
<Steps steps={steps1} {current} radius="full" />

<div class="mt-8 px-4 mb-4 font-bold text-lg">带完成步骤</div>
<Steps steps={steps2} {current} />

<div class="mt-8 px-4 mb-4 font-bold text-lg">带图标 && 完成步骤</div>
<Steps steps={steps3} {current} />

<div class="mt-8 px-4 mb-4 font-bold text-lg">步骤栏区域使用文字</div>
<Steps steps={steps7} {current} />

<div class="mt-8 px-4 mb-4 font-bold text-lg">步骤栏区域使用图片</div>
<Steps steps={steps8} {current} />
<Steps steps={steps8} radius="full" {current} />
<Divider />

<div class="mt-4 px-4 mb-4 font-bold text-2xl">纵向排列</div>
<div class="mt-8 px-4 mb-4 font-bold text-lg">不同圆角</div>
<div class="flex justify-around">
	<Steps {steps} {current} vertical />
	<Steps {steps} {current} radius="none" vertical />
	<Steps {steps} {current} radius="full" vertical />
</div>

<div class="mt-8 px-4 mb-4 font-bold text-lg">图标不同边框</div>
<div class="flex justify-around">
	<Steps steps={steps1} {current} vertical />
	<Steps steps={steps1} {current} vertical radius="full" barBorder={false} />
</div>
<Divider px="8" />
<div class="flex justify-around">
	<Steps steps={steps1} {current} vertical barBorder={false} radius="none" />
	<Steps steps={steps1} {current} vertical radius="none" />
</div>
<Divider px="8" />
<div class="flex justify-around">
	<Steps steps={steps1} {current} vertical radius="xl" />
	<Steps steps={steps1} {current} vertical radius="full" />
</div>

<div class="mt-8 px-4 mb-4 font-bold text-lg">带描述信息</div>
<Steps steps={steps4} {current} vertical />
<Divider px="8" />
<Steps steps={steps5} {current} vertical />

<div class="mt-8 px-4 mb-4 font-bold text-lg">带完成步骤</div>
<Steps steps={steps6} {current} vertical />

<div class="mt-8 px-4 mb-4 font-bold text-lg">步骤栏区域使用文字</div>
<Steps steps={steps7} {current} vertical />

<div class="mt-8 px-4 mb-4 font-bold text-lg">步骤栏区域使用图片</div>
<div class="flex justify-around">
	<Steps steps={steps8} {current} vertical />
	<Steps steps={steps8} {current} radius="full" vertical />
</div>

<div class="mt-8 px-4 mb-4 font-bold text-lg">内容区域注入元素</div>
<Steps steps={steps9} {current} vertical />

<div class="flex sticky bottom-0 z-10 bg-white/60 dark:bg-gray1/60 backdrop-blur">
	<div class="flex-1">
		<Button fill="lineTheme" on:click={preFun}>上一步</Button>
	</div>
	<div class="flex-1">
		<Button fill="lineTheme" on:click={nextFun}>下一步</Button>
	</div>
</div>

<!-- injCom1.svelte -->
<!-- <div class="text-primary dark:text-dark text-sm">
    <div>此处以组件形式注入一张图片</div>
    <div class="rounded-full overflow-hidden h-20 w-20">
        <img src="./assets/images/avatar_1.jpg" alt="" />
    </div>
</div> -->

<!-- injCom2.svelte -->
<!-- <script>
    import { Button, Icon, Avatar } from 'stdf';
</script>

<div class="text-primary dark:text-dark text-sm">此处以组件形式注入一些内容</div>
<div class="flex items-center justify-between">
    <Button size="full" heightIn="2" injClass="px-4">按钮</Button>
    <Avatar image="./assets/images/avatar_1.jpg" size="sm" />
    <Icon name="ri-money-cny-circle-line" theme />
    <Icon name="ri-fingerprint-line" theme />
</div> -->
