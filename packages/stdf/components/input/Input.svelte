<script>
	import { createEventDispatcher, getContext } from 'svelte';
	import Icon from '../icon/Icon.svelte';
	import zh_CN from '../../lang/zh_CN';
	// 定义事件派发器
	// Define event dispatcher
	const dispatch = createEventDispatcher();

	// 当前语言
	// current language
	const currentLang = getContext('STDF_lang') || zh_CN;
	const commonLang = currentLang.common;
	const inputLang = currentLang.input;

	// 标题
	// Title
	export let title = '';

	// 标题位置，out/in/none
	// Title position, out/in/none
	export let titlePosition = 'out';

	// 输入框文字位置，left/right
	// Input box text position, left/right
	export let inputPosition = 'left';

	// 输入框占位符
	// Input box placeholder
	export let placeholder = '';

	// 圆角风格：none/base/xl/full
	// Corner style: none/base/xl/full
	export let radius = 'base';

	//标签 1 - 6 内容
	//Label 1 - 6 content
	export let label1 = '';
	export let label2 = '';
	export let label3 = '';
	export let label4 = '';
	export let label5 = '';
	export let label6 = '';

	// 提示文字
	// Tip text
	export let tip = '';

	// 数据 1 - 3 内容
	// Data 1 - 3 content
	export let data1 = '';
	export let data2 = '';
	export let data3 = '';

	// 输入框值
	// Input box value
	export let value = '';

	// 是否显示清除按钮
	// Whether to show the clear button
	export let clear = false;

	// 输入框风格，块/线
	// Input box style, block/line
	export let inputStyle = 'block';

	//线性动画 none/center/left
	//Linear animation none/center/left
	export let lineTransition = 'none';

	// 过渡时间fast/base/slow/slower
	// Transition time fast/base/slow/slower
	export let duration = 'base';

	// 是否开启自动填充功能
	// Whether to enable automatic filling function
	export let autocomplete = true;

	//垂直间距
	//Vertical spacing
	export let py = '2';

	// 是否禁用
	// Whether to disable
	export let disabled = false;

	// 状态：theme/success/warning/error/info
	// Status: theme/success/warning/error/info
	export let state = 'theme';

	// 输入框类型，文本/小数/邮箱/不显示/整数/搜索/电话/链接/密码/数字
	// Input box type, text/decimal/email/none/numeric/search/tel/url/password/number
	export let type = 'text';

	// 输入模式
	// Input mode
	export let inputmode = '';

	// 最大长度
	// Maximum length
	export let maxlength = 24;

	//针对 textarea 最大长度
	//For textarea maximum length
	export let textareaMaxlength = 200;

	//行数
	//Number of rows
	export let rows = 2;

	// 自动调整大小
	// Automatically adjust size
	export let autosize = false;

	// 是否获取焦点
	// Whether to get focus
	let focus = false;

	// 中文输入上屏标识
	// Chinese input screening flag
	let flag = true;

	//textarea 元素
	//textarea element
	let textareaDom = null;

	// 输入模式判断
	// Input mode judgment
	const modeFun = type => {
		switch (type) {
			case 'password':
				return 'text';
			case 'number':
				return 'decimal';
			case 'textarea':
				return 'text';
			default:
				return type;
		}
	};

	// 输入框类型判断
	// Input box type judgment
	$: mode = inputmode === '' ? modeFun(type) : inputmode;

	// 输入框类型判断
	const typeAction = node => {
		if (type !== 'textarea') {
			node.type = type === 'password' ? 'password' : 'text';
		}
	};

	// 圆角风格样式
	// Corner style style
	const radiusObj = {
		none: 'rounded-none',
		base: 'rounded',
		xl: 'rounded-xl',
		'2xl': 'rounded-2xl',
		full: 'rounded-full',
	};

	// 输入框风格样式
	// Input box style style
	const inputStyleObj = {
		block: 'px-2 ring-2 ring-transparent bg-black/5 dark:bg-white/5 ' + radiusObj[radius] || radiusObj.base,
		line: 'px-1 border-b bg-transparent border-gray7 dark:border-gray5',
	};

	// 状态样式
	// State style
	const stateObj = {
		theme: 'ring-primary dark:ring-dark',
		success: 'ring-success',
		warning: 'ring-warning',
		error: 'ring-error',
		info: 'ring-info',
	};

	// 根据是否获取焦点判断输入框样式
	// Determine the input box style according to whether to get focus
	$: inputStyleFocusObj = {
		block: 'px-2 ring-2 bg-transparent ' + stateObj[state] || stateObj.theme + radiusObj[radius] || radiusObj.base,
		line: 'px-1 border-b bg-transparent border-gray7 dark:border-gray5',
	};

	// 线性动画样式
	// Linear animation style
	const lineTransitionStateObj = {
		theme: 'bg-primary dark:bg-dark ',
		success: 'bg-success',
		warning: 'bg-warning',
		error: 'bg-error',
		info: 'bg-info',
	};

	// 动画时长样式
	// Animation duration style
	const durationObj = {
		fast: 'duration-150',
		base: 'duration-300',
		slow: 'duration-500',
		slower: 'duration-1000',
	};

	// 垂直间距样式
	// Vertical spacing style
	const pyObj = {
		'0': 'py-0',
		'0.5': 'py-0.5',
		'1': 'py-1',
		'2': 'py-2',
		'3': 'py-3',
		'4': 'py-4',
		'6': 'py-6',
	};

	// 获取焦点是派发事件
	// Get focus to dispatch events
	const onFocus = () => {
		focus = true;
		dispatch('focus', value);
	};

	// 失去焦点时派发事件
	// Dispatch events when focus is lost
	const onBlur = () => {
		focus = false;
		dispatch('blur', value);
	};

	// 输入内容变化时触发
	// Triggered when input content changes
	const valueChangeFun = e => {
		//处理拼音输入时，内容上屏后才做校验
		//Handle pinyin input, content screening after validation
		setTimeout(function () {
			if (flag) {
				if (type === 'textarea' && autosize) {
					textareaDom.style.height = textareaDom.scrollHeight + 'px';
				}
				if (type === 'textarea' && e.target.value.length > textareaMaxlength) {
					//去除最后一个字符
					//Remove the last character
					e.target.value = e.target.value.substring(0, textareaMaxlength);
				}
				if (type !== 'textarea' && e.target.value.length > maxlength) {
					//去除最后一个字符
					//Remove the last character
					e.target.value = e.target.value.substring(0, maxlength);
				}
				if (type === 'decimal' || type === 'number') {
					// 数字
					// Number
					value = e.target.value.replace(/[^\d^.]+/g, '');
					// value = e.target.value.replace(/[^\d^\.]+/g, '');
				} else if (type === 'numeric') {
					// 整数
					// Integer
					value = e.target.value.replace(/[^\d]/g, '');
				} else {
					value = e.target.value;
				}
				dispatch('change', value);
			}
		}, 0);
	};

	//拼音输入时，文字还未上屏触发
	//Triggered when the text has not been screened during pinyin input
	const compositionendFun = () => {
		flag = true;
	};

	//拼音输入时，文字完成上屏触发
	//Triggered when the text is completed during pinyin input
	const compositionstartFun = () => {
		flag = false;
	};

	//清除时触发
	//Triggered when cleared
	const clearFun = () => {
		value = '';
		dispatch('clear');
	};

	//点击标签 1 - 6 时派发事件
	//Dispatch events when clicking labels 1 - 6
	const clickLabel1Fun = () => {
		dispatch('clicklabel1');
	};
	const clickLabel2Fun = () => {
		dispatch('clicklabel2');
	};
	const clickLabel3Fun = () => {
		dispatch('clicklabel3');
	};
	const clickLabel4Fun = () => {
		dispatch('clicklabel4');
	};
	const clickLabel5Fun = () => {
		dispatch('clicklabel5');
	};
	const clickLabel6Fun = () => {
		dispatch('clicklabel6');
	};
</script>

<div class={`px-2 ${pyObj[py] || pyObj['2']}`}>
	<label>
		<div class={`flex px-2 ${title === '' ? 'justify-end' : 'justify-between'}`}>
			{#if titlePosition === 'out'}
				{#if title === ''}
					<!-- none -->
				{:else if title === 'slot'}
					<slot name="title">title {commonLang.slotEmpty}</slot>
				{:else}
					<div class="text-sm font-semibold mb-1">{title}</div>
				{/if}
			{/if}
			<div class="flex space-x-2 text-xs">
				{#if data1 === ''}
					<!-- none -->
				{:else if data1 === 'slot'}
					<slot name="data1">data1 {commonLang.slotEmpty}</slot>
				{:else}
					{data1}
				{/if}
				{#if data2 === ''}
					<!-- none -->
				{:else if data2 === 'slot'}
					<slot name="data2">data2 {commonLang.slotEmpty}</slot>
				{:else}
					{data2}
				{/if}
			</div>
		</div>
		<div
			class={`flex items-center my-0.5 space-x-1 text-sm relative transition-all whitespace-nowrap ${
				durationObj[duration] || durationObj.base
			} ${titlePosition === 'in' ? 'py-1' : 'py-3'} ${
				focus ? inputStyleFocusObj[inputStyle] || inputStyleFocusObj.block : inputStyleObj[inputStyle] || inputStyleObj.block
			} ${inputStyle === 'block' ? radiusObj[radius] || radiusObj.base : ''}`}
		>
			{#if label1 === ''}
				<!-- none -->
			{:else if label1 === 'slot'}
				<slot name="label1">label1 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div on:click|preventDefault={clickLabel1Fun}>
					<Icon {...label1} />
				</div>
			{/if}
			{#if label2 === ''}
				<!-- none -->
			{:else if label2 === 'slot'}
				<slot name="label2">label2 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div class="text-sm" on:click|preventDefault={clickLabel2Fun}>
					{label2}
				</div>
			{/if}
			{#if label3 === ''}
				<!-- none -->
			{:else if label3 === 'slot'}
				<slot name="label3">label3 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div on:click|preventDefault={clickLabel3Fun}>
					<Icon {...label3} />
				</div>
			{/if}
			<div class="flex flex-col grow">
				{#if titlePosition === 'in'}
					<div class="text-gray6 text-xs">{title}</div>
				{/if}
				<div class="flex space-x-1">
					<form action="" class="w-full">
						{#if type === 'textarea'}
							<textarea
								bind:value
								use:typeAction
								{rows}
								inputmode={mode}
								placeholder={placeholder !== '' ? placeholder : title !== '' ? inputLang.pleaseInput + ' ' + title : ''}
								class={`w-full focus:outline-none bg-transparent font-semibold ${inputPosition === 'left' ? 'text-left' : 'text-right'} ${
									disabled ? 'cursor-not-allowed opacity-50' : ''
								}`}
								on:focus={onFocus}
								on:blur={onBlur}
								on:input={valueChangeFun}
								on:compositionend={compositionendFun}
								on:compositionstart={compositionstartFun}
								{autocomplete}
								{disabled}
								bind:this={textareaDom}
							/>
						{:else}
							<input
								bind:value
								use:typeAction
								inputmode={mode}
								placeholder={placeholder !== '' ? placeholder : title !== '' ? inputLang.pleaseInput + ' ' + title : ''}
								class={`w-full focus:outline-none bg-transparent font-semibold whitespace-normal ${
									inputPosition === 'left' ? 'text-left' : 'text-right'
								} ${disabled ? 'cursor-not-allowed opacity-50' : ''}`}
								on:focus={onFocus}
								on:blur={onBlur}
								on:input={valueChangeFun}
								on:compositionend={compositionendFun}
								on:compositionstart={compositionstartFun}
								{autocomplete}
								{disabled}
							/>
						{/if}
					</form>
					{#if clear && value !== ''}
						<!-- svelte-ignore a11y-click-events-have-key-events -->
						<!-- svelte-ignore a11y-no-static-element-interactions -->
						<div on:click|preventDefault={clearFun}>
							<Icon name="ri-close-circle-fill" size={16} alpha={0.3} />
						</div>
					{/if}
				</div>
			</div>
			{#if label4 === ''}
				<!-- none -->
			{:else if label4 === 'slot'}
				<slot name="label4">label4 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div on:click|preventDefault={clickLabel4Fun}>
					<Icon {...label4} />
				</div>
			{/if}
			{#if label5 === ''}
				<!-- none -->
			{:else if label5 === 'slot'}
				<slot name="label5">label5 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div class="text-sm" on:click|preventDefault={clickLabel5Fun}>
					{label5}
				</div>
			{/if}
			{#if label6 === ''}
				<!-- none -->
			{:else if label6 === 'slot'}
				<slot name="label6">label6 {commonLang.slotEmpty}</slot>
			{:else}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div on:click|preventDefault={clickLabel6Fun}>
					<Icon {...label6} />
				</div>
			{/if}
			{#if inputStyle === 'line'}
				<div
					class={`h-[2px] absolute -bottom-px ${lineTransition === 'none' ? 'transition-colors' : 'transition-all'} ${
						durationObj[duration] || durationObj.base
					} ${!focus && lineTransition === 'none' && 'bg-transparent w-full'} ${
						focus && lineTransition === 'none' && `${lineTransitionStateObj[state] || lineTransitionStateObj.theme} w-full`
					} ${!focus && lineTransition !== 'none' && `w-0 ${lineTransitionStateObj[state] || lineTransitionStateObj.theme}`} ${
						focus && lineTransition !== 'none' && `w-full ${lineTransitionStateObj[state] || lineTransitionStateObj.theme}`
					}`}
					style={lineTransition === 'center'
						? 'left:50%;transform:translateX(calc( -50% - 0.25rem ));-webkit-transform:translateX(calc( -50% - 0.25rem ));'
						: 'left:0;transform:translateX( -0.25rem );-webkit-transform:translateX( -0.25rem );'}
				/>
			{/if}
		</div>
		<div class={`flex  px-2 text-gay6 ${tip === '' ? 'justify-end' : 'justify-between'}`}>
			{#if tip === ''}
				<!-- none -->
			{:else if tip === 'slot'}
				<slot name="tip">tip {commonLang.slotEmpty}</slot>
			{:else}
				<div class="text-sm text-gray6">
					{tip}
				</div>
			{/if}
			{#if data3 === ''}
				<!-- none -->
			{:else if data3 === 'slot'}
				<slot name="data3">data3 {commonLang.slotEmpty}</slot>
			{:else}
				<div class="text-xs">
					{data3}
				</div>
			{/if}
		</div>
	</label>
</div>
