<!-- Calendar Demo -->
<script>
	import { Cell, Calendar } from 'stdf';

	let visible1 = false;
	let visible2 = false;
	let visible3 = false;
	let visible4 = false;
	let visible5 = false;
	let visible6 = false;
	let visible7 = false;
	let visible8 = false;
	let visible9 = false;
	let visible10 = false;
	let visible11 = false;
	let visible12 = false;
	let visible13 = false;
	let visible14 = false;
	let visible15 = false;
	let visible16 = false;
	let visible17 = false;
	let visible18 = false;
	let visible19 = false;
	let visible20 = false;
	let visible21 = false;
	let visible22 = false;
	let visible23 = false;

	// 随机取出当前日期后的6天，组成 infoDates 数组，其中 date 格式为 YYYYMMDD，月和日补足2位
	const now = new Date();
	const infoDates = [];
	for (let i = 0; i < 6; i++) {
		const date = new Date(now.getTime() + i * 24 * 60 * 60 * 1000);
		infoDates.push(
			`${date.getFullYear()}${(date.getMonth() + 1).toString().padStart(2, '0')}${date.getDate().toString().padStart(2, '0')}`,
		);
	}
	// 循环 infoDates ，按照顺序，将每一项转为对象，date 为日期，info分别为出发、入住、购物、 拍照、离店、回程
	infoDates.forEach((date, index) => {
		infoDates[index] = {
			date,
			info: ['出发', '入住', '购物', '拍照', '离店', '回程'][index],
		};
	});

	// 获取当前日期的前7天和后7天共14天，组成数组 disabledDates，其中 date 格式为 YYYYMMDD，月和日补足2位
	const disabledDates = [];
	const before7 = new Date(now.getTime() - 7 * 24 * 60 * 60 * 1000);
	for (let i = 0; i < 14; i++) {
		const date = new Date(before7.getTime() + i * 24 * 60 * 60 * 1000);
		disabledDates.push(
			`${date.getFullYear()}${(date.getMonth() + 1).toString().padStart(2, '0')}${date.getDate().toString().padStart(2, '0')}`,
		);
	}
	// 传入数字 n，返回当前月份往前推第 n 个月的月份，格式为 YYYYMM，月份补足2位
	const getInitMonth = n => {
		const now = new Date();
		const year = now.getFullYear();
		const month = now.getMonth() + 1;
		const newMonth = month - n;
		if (newMonth > 0) {
			return `${year}${newMonth.toString().padStart(2, '0')}`;
		} else {
			return `${year - 1}${(12 + newMonth).toString().padStart(2, '0')}`;
		}
	};
	const initMonth = getInitMonth(3);

	const quickSelects = ['week', 'month', 'quarter', -3, -7, -30, 3, 7, 30];
	const quickSelectsDay = [-5, -2, 3, 7];

	let selectedDates = [];
	const getSelectedDatesFunc = e => {
		selectedDates = e.detail.dates;
	};

	let selectedFormatDates = [];
	const getSelectedFormatDatesFunc = e => {
		selectedFormatDates = e.detail.dates;
	};
</script>

<div class="py-4">
	<Cell title="基础用法" on:click={() => (visible1 = true)} />
	<Calendar bind:visible={visible1} />

	<Cell title="多选" on:click={() => (visible7 = true)} />
	<Calendar bind:visible={visible7} mode="multiple" />

	<Cell title="范围选择" on:click={() => (visible8 = true)} />
	<Calendar bind:visible={visible8} mode="range" />

	<Cell title="从周日开始" on:click={() => (visible2 = true)} />
	<Calendar bind:visible={visible2} startSunday />

	<Cell title="周末文字标红" on:click={() => (visible3 = true)} />
	<Calendar bind:visible={visible3} weekendRed />

	<Cell title="不使用卡片样式且加水印" on:click={() => (visible4 = true)} />
	<Calendar bind:visible={visible4} monthCard={false} monthMark />

	<Cell title="高一点" on:click={() => (visible5 = true)} />
	<Calendar bind:visible={visible5} height={60} />

	<Cell title="自定义显示信息的日期" on:click={() => (visible6 = true)} />
	<Calendar bind:visible={visible6} {infoDates} />

	<Cell title="不要圆角" on:click={() => (visible9 = true)} />
	<Calendar bind:visible={visible9} mode="range" radius="none" />

	<Cell title="加大圆角" on:click={() => (visible10 = true)} />
	<Calendar bind:visible={visible10} mode="range" radius="2xl" />

	<Cell title="滚动时关闭动画" on:click={() => (visible18 = true)} />
	<Calendar bind:visible={visible18} useAnimation={false} />

	<Cell title="配置确认按钮样式" on:click={() => (visible11 = true)} />
	<Calendar bind:visible={visible11} button={{ radius: 'full' }} />

	<Cell title="顶部来点圆角" on:click={() => (visible19 = true)} />
	<Calendar bind:visible={visible19} popup={{ radius: 'xl' }} />

	<Cell title="定义开始与结束月" on:click={() => (visible12 = true)} />
	<Calendar bind:visible={visible12} startMonth="202101" endMonth="202106" />

	<Cell title="自定义不可选日期" on:click={() => (visible13 = true)} />
	<Calendar bind:visible={visible13} {disabledDates} mode="range" />

	<Cell title="多选或范围选择时不显示已选天数" on:click={() => (visible14 = true)} />
	<Calendar bind:visible={visible14} mode="range" showSelectedDay={false} />

	<Cell title="自定义初始显示月份" subTitle="开始月份为当前月份前第三个月" on:click={() => (visible15 = true)} />
	<Calendar bind:visible={visible15} {initMonth} />

	<Cell title="展示一些快速选择项" on:click={() => (visible16 = true)} />
	<Calendar bind:visible={visible16} mode="range" {quickSelects} />

	<Cell title="快速选择天数时包含当天" on:click={() => (visible23 = true)} />
	<Calendar bind:visible={visible23} mode="range" quickSelects={quickSelectsDay} includeToday />

	<Cell title="从周日开始快速选择本周" on:click={() => (visible17 = true)} />
	<Calendar bind:visible={visible17} mode="range" startSunday quickSelects={['week']} />

	<div class="px-4">
		{#if selectedDates.length}
			当前选定了以下共 {selectedDates.length} 天：
		{:else}
			<div>请选定日期</div>
		{/if}
	</div>
	<div class="grid grid-cols-4 gap-2 p-2 text-primary dark:text-dark">
		{#each selectedDates as item}
			<div class="text-center">{item}</div>
		{/each}
	</div>
	<Cell title="获取返回的选定日期" on:click={() => (visible20 = true)} />
	<Calendar bind:visible={visible20} mode="range" on:confirm={getSelectedDatesFunc} />

	<div class="px-4">
		{#if selectedFormatDates.length}
			当前选定了以下共 {selectedFormatDates.length} 天：
		{:else}
			<div>请选定日期</div>
		{/if}
	</div>
	<div class="grid grid-cols-3 gap-2 p-2 text-primary dark:text-dark text-sm">
		{#each selectedFormatDates as item}
			<div class="text-center">{item}</div>
		{/each}
	</div>
	<Cell title="自定义返回的日期格式" on:click={() => (visible21 = true)} />
	<Calendar bind:visible={visible21} mode="range" outFormat="Y年M月D日" on:confirm={getSelectedFormatDatesFunc} />

	<Cell title="今日日期关闭高亮显示" on:click={() => (visible22 = true)} />
	<Calendar bind:visible={visible22} highlightToday={false} />
</div>
