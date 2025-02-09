<script>
    let {
        csen10 = $bindable(false),
        csen11 = $bindable(false),
        csen12 = $bindable(false),
        csen20 = $bindable(false),
        csen19 = $bindable(false),
        csen79 = $bindable(false),
        csen146 = $bindable(false),
        csen171 = $bindable(false),
        csen177 = $bindable(false),
        csen179 = $bindable(false),
        csen122 = $bindable(false),
        csen174 = $bindable(false),
        csen175 = $bindable(false),
        ecen21 = $bindable(false),
        ecen50 = $bindable(false),
        ecen153 = $bindable(false),
        openElectives = $bindable(false),
    } = $props();
</script>

<div class="sidebar">
    <h2>Select classes you've taken</h2>
    <div class="sidebar-elements">
        <div class="sidebar-section">
            <h3>CSEN Cores</h3>
            <input type="checkbox" id="csen10" bind:checked={csen10} />
            <label for="csen10">CSEN 10</label><br />
            <input type="checkbox" id="csen11" bind:checked={csen11} />
            <label for="csen11">CSEN 11</label><br />
            <input type="checkbox" id="csen12" bind:checked={csen12} />
            <label for="csen12">CSEN 12</label><br />
            <input type="checkbox" id="csen20" bind:checked={csen20} />
            <label for="csen20">CSEN 20</label><br />
            <input type="checkbox" id="csen19" bind:checked={csen19} />
            <label for="csen19">CSEN 19</label><br />
            <input type="checkbox" id="csen79" bind:checked={csen79} />
            <label for="csen79">CSEN 79</label><br />
            <input type="checkbox" id="csen146" bind:checked={csen146} />
            <label for="csen146">CSEN 146</label><br />
            <input type="checkbox" id="csen171" bind:checked={csen171} />
            <label for="csen171">CSEN 171</label><br />
            <input type="checkbox" id="csen177" bind:checked={csen177} />
            <label for="csen177">CSEN 177</label><br />
            <input type="checkbox" id="csen179" bind:checked={csen179} />
            <label for="csen179">CSEN 179</label><br />
            <input type="checkbox" id="csen122" bind:checked={csen122} />
            <label for="csen122">CSEN 122</label><br />
            <input type="checkbox" id="csen174" bind:checked={csen174} />
            <label for="csen174">CSEN 174</label><br />
            <input type="checkbox" id="csen175" bind:checked={csen175} />
            <label for="csen175">CSEN 175</label><br />
        </div>
        <div class="sidebar-section">
            <h3>ECEN Cores</h3>
            <input type="checkbox" id="ecen21" bind:checked={ecen21} />
            <label for="ecen21">ECEN 21</label><br />
            <input type="checkbox" id="ecen21" bind:checked={ecen50} />
            <label for="ecen50">ECEN 50</label><br />
            <input type="checkbox" id="ecen21" bind:checked={ecen153} />
            <label for="ecen153">ECEN 153</label><br />
        </div>
        <div class="sidebar-section">
            <h3>Electives</h3>
            <button onclick={() => (openElectives = !openElectives)}
                >Open Electives Picker</button
            >
        </div>
    </div>
</div>

<style>
    .sidebar {
        width: 20%;
        padding: 1rem;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
        margin-right: 1rem;
    }
    h3 {
        margin-top: 1rem;
        margin-bottom: 0.5rem;
    }
</style>
