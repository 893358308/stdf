<!-- Slider Demo -->
<script>
	import { Slider, Icon } from 'stdf';

	let value = 20;
	const onChangeFun = e => {
		value = e.detail;
	};
	let valueRange = [50, 60];
	const onChangeRangeFun = e => {
		valueRange = e.detail;
	};
	//生成指定数字之间的随机数组成的数组
	const randomArray = (min, max, length) => {
		let arr = [];
		for (let i = 0; i < length; i++) {
			arr.push(Math.floor(Math.random() * (max - min + 1) + min));
		}
		return arr;
	};
	//将数组递增或递减排序
	const sortArray = (arr, isAsc) => {
		return arr.sort((a, b) => (isAsc ? a - b : b - a));
	};
	const barList1 = sortArray(randomArray(2, 60, 20), true);
	const barList2 = sortArray(randomArray(2, 60, 20), false);
	const barList = [...barList1, ...barList2];
	let valueBar = 70;
	const onChangeBarFun = e => {
		valueBar = e.detail;
	};
</script>

<div class="mx-4 mt-8 font-bold text-lg">基础用法</div>
<div class="px-6 py-4">
	<Slider />
</div>
<div class="mx-4 mt-8 font-bold text-lg">监听 value</div>
<div class="px-6 py-4">
	<Slider on:change={onChangeFun} {value} />
	当前值：{value}
</div>
<div class="mx-4 mt-8 font-bold text-lg">步长为 5</div>
<div class="px-6 py-4">
	<Slider step={5} />
</div>
<div class="mx-4 mt-8 font-bold text-lg">步长为 0.1</div>
<div class="px-6 py-4">
	<Slider step={0.1} value={0.2} minRange={0} maxRange={1} />
</div>
<div class="mx-4 mt-8 font-bold text-lg">设定可选范围（60-80）</div>
<div class="px-6 py-4">
	<Slider value={68} minRange={60} maxRange={80} />
</div>
<div class="mx-4 mt-8 font-bold text-lg">区间选择</div>
<div class="px-6 py-4">
	<Slider isRange />
</div>
<div class="mx-4 mt-8 font-bold text-lg">区间设定可选范围（40-80）</div>
<div class="px-6 py-4">
	<Slider isRange minRange={40} maxRange={80} startValue={valueRange[0]} endValue={valueRange[1]} on:change={onChangeRangeFun} />
	当前区间：{valueRange[0]} - {valueRange[1]}
</div>
<div class="mx-4 mt-8 font-bold text-lg">不同圆角</div>
<div class="px-6 py-4">
	<Slider radius="base" />
</div>
<div class="px-6 py-4">
	<Slider radius="none" />
</div>
<div class="px-6 py-4">
	<Slider radius="base" isRange />
</div>
<div class="mx-4 mt-8 font-bold text-lg">线框滑块</div>
<div class="px-6 py-4">
	<Slider lineBlock radius="base" />
</div>
<div class="px-6 py-4">
	<Slider lineBlock isRange />
</div>
<div class="mx-4 mt-8 font-bold text-lg">一直显示 Tip</div>
<div class="px-6 py-4">
	<Slider showTip="always" />
</div>
<div class="px-6 py-4">
	<Slider showTip="always" isRange />
</div>
<div class="px-6 py-4">
	<Slider showTip="always" radius="none" />
</div>
<div class="mx-4 mt-8 font-bold text-lg">不显示 Tip</div>
<div class="px-6 py-4">
	<Slider showTip="never" />
</div>
<div class="mx-4 mt-8 font-bold text-lg">组合布局</div>
<div class="flex space-x-3 p-4">
	<Icon name="ri-volume-mute-line" />
	<div class="grow">
		<Slider />
	</div>
	<Icon name="ri-volume-up-line" />
</div>
<div class="mx-4 mt-8 font-bold text-lg">使用 Slot</div>
<div class="px-6 pt-16">
	<Slider lineBlock showTip="never" useSlot value={valueBar} on:change={onChangeBarFun}>
		<div class="grow relative items-end">
			<div class="flex justify-between items-end overflow-hidden" style="transform: translateY(-30px);">
				{#each barList as item, i}
					<div
						class={`w-1 rounded-full${i / 40 < valueBar / 100 ? ' bg-primary dark:bg-dark' : ' bg-gray8 dark:bg-gray6'}`}
						style="height: {item}px"
					/>
				{/each}
			</div>
		</div>
	</Slider>
</div>
<div class="mx-4 mt-8 font-bold text-lg">禁用</div>
<div class="px-6 py-4">
	<Slider disabled />
</div>
<div class="mx-4 mt-8 font-bold text-lg">只读</div>
<div class="px-6 py-4">
	<Slider readonly />
</div>
