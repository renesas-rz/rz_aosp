### **Memory map**

Memory map of RZ/V2H EVK DDR 16GByte

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
            <td colspan="3" style="background-color: #e6f7e6"><strong>8064MB</strong></td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_48000000 - 0x0_53CFFFFF</td>
            <td>189MB</td>
        </tr>
        <tr>
            <td>For bootreason</td>
            <td>0x0_53D00000 - 0x0_53D00FFF</td>
            <td>4KB</td>
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
            <td>0x0_58000000 - 0x0_73FFFFFF</td>
            <td>448MB</td>
        </tr>
        <tr>
            <td>cma-MMP</td>
            <td>0x0_74000000 - 0x0_93FFFFFF</td>
            <td>512MB</td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_94000000 - 0x0_BFFFFFFF</td>
            <td>704MB</td>
        </tr>
        <tr>
            <td>OpenCVA</td>
            <td>0x0_C0000000 - 0x0_C7CFFFFF</td>
            <td>125MB</td>
        </tr>
        <tr>
            <td>DRP-Codec</td>
            <td>0x0_C7D00000 - 0x0_C7FFFFFF</td>
            <td>3MB</td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x0_C8000000 - 0x2_3FFFFFFF</td>
            <td>6016MB</td>
        </tr>
        <tr>
            <td rowspan="3"><strong>Bank1</strong></td>
            <td colspan="3" style="background-color: #e6f2ff"><strong>8192MB</strong></td>
        </tr>
        <tr>
            <td>DRP-AI</td>
            <td>0x2_40000000 - 0x2_5FFFFFFF</td>
            <td>512MB</td>
        </tr>
        <tr>
            <td>-</td>
            <td>0x2_60000000 - 0x4_3FFFFFFF</td>
            <td>7680MB</td>
        </tr>
    </tbody>
</table>
</div>
