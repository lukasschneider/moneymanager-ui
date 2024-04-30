<script lang="ts">
    import { 
        createTable, 
        Render, 
        Subscribe,
        createRender,
    } from "svelte-headless-table";
    import {
        addPagination,
        addTableFilter,
    } from "svelte-headless-table/plugins";
    import DataTableActions from "./data-table-actions.svelte";
    import { readable } from "svelte/store";
    import * as Table from "$lib/components/ui/table";
    import { Button } from "$lib/components/ui/button";
    import { Input } from "$lib/components/ui/input";

    type Incomes = {
        id: string;
        title: string;
        source: string;
        category: string;
        date: string;
        value: number;
    }

    type Expense = {
        id: string;
        title: string;
        source: string;
        category: string;
        date: string;
        value: number;
    }
    
    export let data: Incomes[] | Expense[];


    const table = createTable(readable(data), {
        page: addPagination({
            initialPageSize: 9
        }),
        filter: addTableFilter({
            fn: ({ filterValue, value }) =>
            value.toLowerCase().includes(filterValue.toLowerCase()),
        }),
    });
    const columns = table.createColumns([
        table.column({
            accessor: "id",
            header: "ID",
            plugins: {
                filter: {
                    exclude: true,
                },
            },
        }),
        table.column({
            accessor: "title",
            header: "Titel",
        }),
        table.column({
            accessor: "source",
            header: "Quelle",
        }),
        table.column({
            accessor: "category",
            header: "Kategorie",
        }),
        table.column({
            accessor: "date",
            header: "Datum",
        }),
        table.column({
            accessor: "value",
            header: "Betrag",
            cell: ({ value }) => {
                const formatted = new Intl.NumberFormat("de-DE", {
                    style: "currency",
                    currency: "EUR",
                }).format(value);
                return formatted;
            },
            plugins: {
                filter: {
                    exclude: true,
                },
            },
        }),
        table.column({
            accessor: ({ id }) => id,
            header: "",
            cell: ({ value }) => {
                return createRender(DataTableActions, { 
                    id: value 
                });
            },
            plugins: {
                filter: {
                    exclude: true,
                },
            },
        }),
    ]);

    const { 
        headerRows, 
        pageRows, 
        tableAttrs, 
        tableBodyAttrs,
        pluginStates,
    } = table.createViewModel(columns);

    const { 
        hasNextPage, 
        hasPreviousPage, 
        pageIndex 
    } = pluginStates.page;

    const { 
        filterValue 
    } = pluginStates.filter;

</script>
<div class="flex items-center py-4">
    <Input
      class="max-w-sm"
      placeholder="Suche..."
      type="text"
      bind:value={$filterValue}
    />
</div>
<div class="rounded-md border">
    <Table.Root {...$tableAttrs}>
        <Table.Header>
        {#each $headerRows as headerRow}
            <Subscribe rowAttrs={headerRow.attrs()}>
            <Table.Row>
                {#each headerRow.cells as cell (cell.id)}
                <Subscribe attrs={cell.attrs()} let:attrs props={cell.props()}>
                    <Table.Head {...attrs}>
                        {#if cell.id == "value"}
                        <div class="text-right">
                            <Render of={cell.render()} />
                        </div>
                        {:else}
                        <div class="text-left">
                            <Render of={cell.render()} />
                        </div>
                        {/if}
                    </Table.Head>
                </Subscribe>
                {/each}
            </Table.Row>
            </Subscribe>
        {/each}
        </Table.Header>
    <Table.Body {...$tableBodyAttrs}>
        {#each $pageRows as row (row.id)}
            <Subscribe rowAttrs={row.attrs()} let:rowAttrs>
                <Table.Row {...rowAttrs}>
                    {#each row.cells as cell (cell.id)}
                        <Subscribe attrs={cell.attrs()} let:attrs>
                        <Table.Cell {...attrs}>
                        {#if cell.id == "value"}
                        <div class="text-right">
                            <Render of={cell.render()} />
                        </div>
                        {:else}
                            <Render of={cell.render()} />
                        {/if}
                        </Table.Cell>
                    </Subscribe>
                    {/each}
                </Table.Row>
            </Subscribe>
      {/each}
    </Table.Body>
  </Table.Root>
</div>
<div class="flex items-center justify-end space-x-4 py-4">
    <Button
    variant="outline"
    size="sm"
    on:click={() => ($pageIndex = $pageIndex - 1)}
    disabled={!$hasPreviousPage}>Previous</Button
    >
    <Button
    variant="outline"
    size="sm"
    disabled={!$hasNextPage}
    on:click={() => ($pageIndex = $pageIndex + 1)}>Next</Button
    >
</div>
