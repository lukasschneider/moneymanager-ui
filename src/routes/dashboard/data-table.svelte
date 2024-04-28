<script lang="ts">
    import { 
        createTable, 
        Render, 
        Subscribe,
        createRender,
    } from "svelte-headless-table";
    import {
        addPagination
    } from "svelte-headless-table/plugins";
    import DataTableActions from "./data-table-actions.svelte";
    import { readable } from "svelte/store";
    import * as Table from "$lib/components/ui/table";
    import { Button } from "$lib/components/ui/button";


    type Incomes = {
        id: string;
        title: string;
        source: string;
        category: string;
        date: string;
        value: number;
    }

    const data: Incomes[] = [
        {
            id: "e2a71f59-79d5-4128-8cdc-408564068150",
            title: "Gehalt",
            source: "Arbeitgeber",
            category: "Gehalt",
            date: "28.04.2024",
            value: 2500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
        {
            id: "b6010689-d415-4175-92fb-c7b18de6fb87",
            title: "Rückzahlung",
            category: "Rückzahlung",
            source: "Paypal",
            date: "28.04.2024",
            value: 49.99,
        },
        {
            id: "e2a71f59-79d5-4128-8cdc-408564068150",
            title: "Gehalt",
            source: "Arbeitgeber",
            category: "Gehalt",
            date: "28.04.2024",
            value: 2500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
        {
            id: "b6010689-d415-4175-92fb-c7b18de6fb87",
            title: "Rückzahlung",
            category: "Paypal",
            source: "Bank",
            date: "28.04.2024",
            value: 49.99,
        },
        {
            id: "e2a71f59-79d5-4128-8cdc-408564068150",
            title: "Gehalt",
            source: "Arbeitgeber",
            category: "Gehalt",
            date: "28.04.2024",
            value: 2500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
        {
            id: "b6010689-d415-4175-92fb-c7b18de6fb87",
            title: "Rückzahlung",
            category: "Paypal",
            source: "Bank",
            date: "28.04.2024",
            value: 49.99,
        },
        {
            id: "e2a71f59-79d5-4128-8cdc-408564068150",
            title: "Gehalt",
            source: "Arbeitgeber",
            category: "Gehalt",
            date: "28.04.2024",
            value: 2500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
        {
            id: "96975ba9-0343-496c-b265-dfb0b1183d30",
            title: "Zinsen",
            category: "Bankdepot",
            source: "Bank",
            date: "28.04.2024",
            value: 500,
        },
    ];

    const table = createTable(readable(data), {
        page: addPagination({
            initialPageSize: 9
        }),
    });
    const columns = table.createColumns([
        table.column({
            accessor: "id",
            header: "ID",
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
        }),
        table.column({
            accessor: ({ id }) => id,
            header: "",
            cell: ({ value }) => {
                return createRender(DataTableActions, { id: value });
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
</script>
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
                            <Render of={cell.render()} />
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
                        <div class="text-right text-green-600">
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
