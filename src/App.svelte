<script>
    import logo from './assets/svelte.png';
    import "carbon-components-svelte/css/all.css";

    import {
        Button,
        DataTable,
        Modal,
        Toolbar,
        ToolbarBatchActions,
        ToolbarContent,
        ToolbarMenu,
        ToolbarMenuItem,
        ToolbarSearch,
    } from "carbon-components-svelte";
    import Save16 from "carbon-icons-svelte/lib/Save16";

    let theme = "g10"; // "white" | "g10" | "g80" | "g90" | "g100"

    $: document.documentElement.setAttribute("theme", theme);

    let open = false;

    const headers = [
        {key: "name", value: "Name"},
        {key: "port", value: "Port"},
        {key: "rule", value: "Rule"},
    ];

    const rows = [
        {id: "a", name: "Load Balancer 3", port: 3000, rule: "Round robin"},
        {id: "b", name: "Load Balancer 1", port: 443, rule: "Round robin"},
        {id: "c", name: "Load Balancer 2", port: 80, rule: "DNS delegation"},
        {id: "d", name: "Load Balancer 6", port: 3000, rule: "Round robin"},
        {id: "e", name: "Load Balancer 4", port: 443, rule: "Round robin"},
        {id: "f", name: "Load Balancer 5", port: 80, rule: "DNS delegation"},
    ];

    let selectedRowIds = [rows[0].id, rows[1].id];

    // $: console.log("selectedRowIds", selectedRowIds);

</script>

<main>
    <img src={logo} alt="Svelte Logo"/>
    <h1>Hello world!</h1>
    <p>param</p>
    <Button on:click={() => (open = true)}>创建对话框</Button>
    <Modal
            bind:open
            modalHeading="创建对话框"
            primaryButtonText="确认"
            secondaryButtonText="取消"
            on:click:button--secondary={() => (open = false)}
            on:open
            on:close
            on:submit
    >
        <p>测试一下对话框的性能.</p>
    </Modal>

    <DataTable batchSelection bind:selectedRowIds {headers} {rows}>
        <Toolbar>
            <ToolbarBatchActions>
                <Button icon={Save16}>Save</Button>
            </ToolbarBatchActions>
            <ToolbarContent>
                <ToolbarSearch/>
                <ToolbarMenu>
                    <ToolbarMenuItem primaryFocus>Restart all</ToolbarMenuItem>
                    <ToolbarMenuItem href="https://cloud.ibm.com/docs/loadbalancer-service">
                        API documentation
                    </ToolbarMenuItem>
                    <ToolbarMenuItem danger>Stop all</ToolbarMenuItem>
                </ToolbarMenu>
                <Button>Create balancer</Button>
            </ToolbarContent>
        </Toolbar>
    </DataTable>
</main>

<style>

    main {
        text-align: center;
        padding: 1em;
        margin: 0 auto;
    }

    img {
        height: 8rem;
        width: 8rem;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4rem;
        font-weight: 100;
        line-height: 1.1;
        margin: 2rem auto;
        max-width: 14rem;
    }

    p {
        max-width: 14rem;
        margin: 1rem auto;
        line-height: 1.35;
    }

    @media (min-width: 480px) {
        h1 {
            max-width: none;
        }

        p {
            max-width: none;
        }
    }
</style>
