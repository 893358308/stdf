<script>
	import { createEventDispatcher, getContext } from 'svelte';
	import Icon from '../icon/Icon.svelte';
	import Switch from '../switch/Switch.svelte';
	import zh_CN from '../../lang/zh_CN';

	// 定义事件派发器
	// Define event dispatcher
	const dispatch = createEventDispatcher();

	// 当前语言
	// current language
	const currentLang = getContext('STDF_lang') || zh_CN;
	const commonLang = currentLang.common;

	// 标题
	// Title
	export let title = '';

	// 右侧详情
	// Right side details
	export let detail = '';

	// 右侧 arrow，none，switch props,icon props,slot
	// Right arrow, none, switch props, icon props, slot
	export let right = 'arrow';

	// 左侧 '',icon props,slot
	// Left '', icon props, slot
	export let left = '';

	// 左侧下方描述
	// Left side description
	export let subTitle = '';

	// 右侧下方描述
	// Right side description
	export let info = '';

	// 是否显示底部分割线
	// Whether to show the bottom line
	export let line = false;

	// 上下边距
	// Top and bottom margin
	export let my = '4';

	// 左右间距
	// Left and right margin
	export let mx = '2';

	// 圆角风格
	// Rounded style
	export let radius = 'lg';

	// 开关状态
	// Switch status
	export let switcheck = false;

	// 阴影，none/sm/md/lg/xl/2xl
	// Shadow, none/sm/md/lg/xl/2xl
	export let shadow = 'sm';

	// 注入 CSS
	// Inject CSS
	export let injClass = '';

	// 是否开启关爱版
	// Whether to open the care version
	export let love = false;

	// 圆角风格样式
	// Rounded style style
	const radiusObj = {
		none: ' rounded-none',
		base: ' rounded',
		md: ' rounded-md',
		lg: ' rounded-lg',
		xl: ' rounded-xl',
		'2xl': ' rounded-2xl',
		full: ' rounded-full',
	};

	// 阴影风格样式
	// Shadow style style
	const shadowClass = {
		none: ' shadow-none',
		sm: ' shadow-sm dark:shadow-white/5',
		base: ' shadow dark:shadow-white/10',
		md: ' shadow-md dark:shadow-white/10',
		lg: ' shadow-lg dark:shadow-white/10',
		xl: ' shadow-xl dark:shadow-white/10',
		'2xl': ' shadow-2xl dark:shadow-white/25',
	};

	// 左右间距样式
	// Left and right margin style
	const mxClass = {
		'0': ' mx-0',
		'1': ' mx-1',
		'2': ' mx-2',
		'3': ' mx-3',
		'4': ' mx-4',
		'6': ' mx-6',
		'8': ' mx-8',
	};

	// 上下边距样式
	// Top and bottom margin style
	const myClass = {
		'0': ' my-0',
		'1': ' my-1',
		'2': ' my-2',
		'3': ' my-3',
		'4': ' my-4',
		'6': ' my-6',
		'8': ' my-8',
	};

	// 点击事件
	// Click event
	const setClickFun = () => {
		if (right?.constructor === Object && right.type === 'switch' && !right.switch?.disabled) {
			switcheck = right.switch?.async ? switcheck : !switcheck;
		}
		// 派发事件
		// Dispatch event
		dispatch('click');
	};
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
	on:click={setClickFun}
	class={`px-4 cursor-pointer bg-white dark:bg-gray1 active:bg-gray8 dark:active:bg-gray4 ${myClass[my] || myClass['4']}${
		mxClass[mx] || mxClass['2']
	}${radiusObj[radius] || radiusObj['lg']} ${shadowClass[shadow] || shadowClass['sm']}${love ? ' text-xl' : ''} ${injClass}`}
>
	<div class={`flex justify-between gap-4 py-4${line && my === '0' ? ' border-b border-black/5 dark:border-white/5' : ''}`}>
		<!-- left -->
		<div class="flex justify-between">
			{#if left === ''}
				<!-- none -->
			{:else if left === 'slot'}
				<slot name="left">
					{commonLang.slotEmpty}
				</slot>
			{:else}
				<div class="mr-1 flex flex-col justify-center">
					<Icon {...left} />
				</div>
			{/if}
			<div class={`flex flex-col ${subTitle === '' ? 'justify-center' : 'justify-between'}`}>
				<div class="font-medium">{title}</div>
				<div class="text-xs text-gray5 dark:text-gray6">{subTitle}</div>
			</div>
		</div>
		<!-- right -->
		<div class="flex justify-between">
			<div class={`flex flex-col ${info === '' ? 'justify-center' : 'justify-between'} text-right `}>
				{#if detail === 'slot'}
					<slot name="detail">
						{commonLang.slotEmpty}
					</slot>
				{:else}
					<div class="text-gray6">{detail}</div>
				{/if}
				<div class="text-xs text-gray5 dark:text-gray6 font-light">{info}</div>
			</div>
			{#if right === 'none'}
				<!-- none -->
			{:else if right === 'arrow'}
				<div class="text-gray6 flex flex-col justify-center">
					<Icon name="ri-arrow-right-s-line" size={love ? 26 : 20} alpha={0.6} top={-2} />
				</div>
			{:else if right?.constructor === Object && right.type === 'switch'}
				<div class="ml-1 flex flex-col justify-center">
					<Switch check={switcheck} {...right.switch} />
				</div>
			{:else if right?.constructor === Object && right.type === 'icon'}
				<div class="ml-1 flex flex-col justify-center">
					<Icon {...right} />
				</div>
			{:else if right === 'slot'}
				<slot name="right">
					{commonLang.slotEmpty}
				</slot>
			{:else}
				<!-- none -->
			{/if}
		</div>
	</div>
</div>
