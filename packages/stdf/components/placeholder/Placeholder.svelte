<script>
	// 上下内边距
	// up down padding
	export let py = '4';

	// 高度
	// height
	export let height = 'full';

	// 圆角风格
	// radius style
	export let radius = 'md';

	// 阴影风格
	// shadow style
	export let shadow = 'none';

	// 注入class
	// inject class
	export let injClass = '';

	// 上下内边距样式
	// up down padding style
	const pyObj = {
		'0': ' py-0',
		'1': ' py-1',
		'2': ' py-2',
		'4': ' py-4',
		'8': ' py-8',
	};

	// 阴影样式
	// shadow style
	const shadowObj = {
		none: ' shadow-none',
		sm: ' shadow-sm',
		md: ' shadow-md',
		lg: ' shadow-lg',
		xl: ' shadow-xl',
		'2xl': ' shadow-2xl',
	};

	// 圆角样式
	// radius style
	const radiusObj = {
		none: ' rounded-none',
		base: ' rounded',
		md: ' rounded-md',
		xl: ' rounded-xl',
		'2xl': ' rounded-2xl',
		'3xl': ' rounded-3xl',
		full: ' rounded-full',
	};

	// 高度样式
	// height style
	const heightObj = {
		full: ' h-full',
		'1': ' h-1',
		'2': ' h-2',
		'4': ' h-4',
		'8': ' h-8',
		'16': ' h-16',
		'24': ' h-24',
		'32': ' h-32',
		'48': ' h-48',
		'64': ' h-64',
		'96': ' h-96',
	};
</script>

<div
	class={`bg-black/5 dark:bg-white/5 flex flex-col justify-center text-center${heightObj[height] || heightObj.full}${
		pyObj[py] || pyObj['4']
	}${radiusObj[radius] || radiusObj.base}${shadowObj[shadow] || shadowObj.none}${injClass === '' ? '' : ` ${injClass}`}`}
>
	<slot />
</div>
