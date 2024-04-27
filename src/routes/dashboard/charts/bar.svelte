<script lang="ts">
	import { scaleLinear } from "d3-scale";

	const data = [
		{
			name: "Jan",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Feb",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Mär",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Apr",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Mai",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Jun",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Jul",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Aug",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Sep",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Okt",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Nov",
			total: Math.floor(Math.random() * 500) + 100,
		},
		{
			name: "Dez",
			total: Math.floor(Math.random() * 500) + 100,
		},
	];

    let width = 500;
    let height = 400;

    const max = function() {
        let v = 0
        for (let i = 0; i < data.length; i++) {
            if (data[i].total >= v) {
                v = data[i].total
            }
        }
        if (v >= 10000) {
            return Math.ceil(v/1000)*1000
        }
        if (v >= 1000) {
            return Math.ceil(v/500)*500
        }
        return Math.ceil(v/100)*100
    }();

    const yTicks = function() {
        let v = [0]
        if (max > 5000 && max <= 10000) {
            for (let i = max; i >= 0; i-=1000) {
                v.push(i)
            }
        } else if (max > 1000 && max <= 5000) {
            for (let i = max; i >= 0; i-=500) {
                v.push(i)
            }
        } else {
            for (let i = max; i >= 0; i-=100) {
                v.push(i)
            }
        }
        return v
    }()

	const xTicks = data.map((d) => d.name);
	const padding = { top: 20, right: 15, bottom: 20, left: 45 };

	function formatMobile(tick: number | string) {
		return `'${tick.toString().slice(-2)}`;
	}

	$: xScale = scaleLinear()
		.domain([0, xTicks.length])
		.range([padding.left, width - padding.right]);

	$: yScale = scaleLinear()
		.domain([0, Math.max.apply(null, yTicks)])
		.range([height - padding.bottom, padding.top]);

	$: innerWidth = width - (padding.left + padding.right);
	$: barWidth = innerWidth / xTicks.length;
</script>

<div class="chart" bind:clientWidth={width} bind:clientHeight={height}>
	<svg>
		<!-- y axis -->
		<g class="axis y-axis">
			{#each yTicks as tick}
				<g class="text-xs" transform="translate(0, {yScale(tick)})">
					<text
						stroke="none"
						font-size="12"
						orientation="left"
						width="60"
						height="310"
						x="57"
						y="-4"
						fill="#888888"
						text-anchor="end"><tspan x="40" dy="0.355em">{tick} €</tspan></text
					>
				</g>
			{/each}
		</g>

		<!-- x axis -->
		<g class="axis x-axis">
			{#each data as point, i}
				<g class="text-xs" transform="translate({xScale(i)},{height})">
					<text
						stroke="none"
						font-size="12"
						orientation="bottom"
						width="531"
						height="30"
						x={barWidth / 2}
						y="-15"
						fill="#888888"
						text-anchor="middle"
						><tspan x={barWidth / 2} dy="0.71em"
							>{width > 380 ? point.name : formatMobile(point.name)}</tspan
						></text
					>
				</g>
			{/each}
		</g>

		<g>
			{#each data as point, i}
				<rect
					class="bg-primary-foreground"
					x={xScale(i) + 2}
					y={yScale(point.total)}
					width={barWidth - 8}
					height={yScale(0) - yScale(point.total)}
					fill="currentColor"
					rx="4"
                    ry="4"
				/>
                <text 
					x={xScale(i) + (barWidth / 2)}
					y={yScale(point.total) - 10}
                    text-anchor="middle"
                    font-size="15" 
                    fill="currentColor">{ point.total }</text>   
			{/each}
		</g>
	</svg>
</div>

<style>
	.chart {
		width: 100%;
		margin: 0 auto;
	}

	svg {
		position: relative;
		width: 100%;
		height: 350px;
	}

	rect {
		max-width: 51px;
	}
</style>
