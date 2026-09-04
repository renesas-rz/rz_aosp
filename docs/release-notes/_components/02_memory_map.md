### **Memory map**

Memory map of SMARC RZ/G3L DDR 2GByte

<div class="table-no-sort" markdown="1">
<table>
    <thead>
        <tr>
            <th>Bank</th>
            <th>Description</th>
            <th>Address Range</th>
            <th>Size</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="12"><strong>Bank0</strong></td>
            <td colspan="3" style="background-color: #e6f2ff"><strong>128MB (reserved)</strong></td>
        </tr>
        <tr>
            <td colspan="3" style="background-color: #e6f7e6"><strong>1920MB</strong></td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_48000000 - 0x0_53D00FFF</td>
            <td>193540KB</td>
        </tr>
        <tr>
            <td>For ramoops</td>
            <td>0x0_53D01000 - 0x0_53E00FFF</td>
            <td>1MB</td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_53E01000 - 0x0_57FFFFFF</td>
            <td>67580KB</td>
        </tr>
        <tr>
            <td>cma</td>
            <td>0x0_58000000 - 0x0_67FFFFFF</td>
            <td>256MB</td>
        </tr>
        <tr>
            <td>cma-MMP</td>
            <td>0x0_68000000 - 0x0_6FFFFFFF</td>
            <td>128MB</td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_70000000 - 0x0_BFFFFFFF</td>
            <td>1280MB</td>
        </tr>
    </tbody>
</table>
</div>
