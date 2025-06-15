# Power BI MCP Server

**Real-time Power BI Desktop integracijos sprendimas per Model Context Protocol (MCP)**

## Aprašymas

Šis MCP serveris leidžia Claude Code Assistant autonomiškai dirbti su Power BI Desktop projektais **real-time režime**. Naudojant TOM (Tabular Object Model) technologiją, galima kurti DAX measures, calculated columns, table relationships ir valdyti modelio struktūrą tiesiogiai atidarytame .pbix faile.

## Funkcionalumas

### 🎯 Real-time Desktop Integration Tools
- **connect_to_desktop_realtime()** - Prisijungti prie Power BI Desktop per TOM
- **create_measure_realtime()** - Sukurti DAX measure tiesiogiai modelyje
- **create_calculated_column_realtime()** - Sukurti calculated column real-time
- **create_relationship_realtime()** - Sukurti table relationships real-time
- **get_desktop_model_info()** - Gauti modelio metadata ir struktūrą
- **execute_dax_desktop_realtime()** - Vykdyti DAX užklausas Desktop modelyje
- **discover_desktop_instances()** - Aptikti Power BI Desktop procesus ir XMLA endpoints

### 🔗 Power BI Service API Tools  
- **connect_to_powerbi()** - Prisijungti prie Power BI Service
- **execute_dax_query_tool()** - Vykdyti DAX užklausas per REST API
- **refresh_dataset_tool()** - Atnaujinti duomenų rinkinius
- **connect_xmla_endpoint()** - Prisijungti prie XMLA endpoint
- **execute_xmla_query_tool()** - Vykdyti XMLA užklausas
- **list_workspace_content()** - Gauti workspace turinį

### 🧮 DAX Optimization Tools
- **optimize_dax_formula()** - Optimizuoti DAX formules
- **generate_time_intelligence_measures()** - Generuoti time intelligence measures rinkinį

### 📊 Resources (Šaltiniai)
- **powerbi://status** - Pilnas MCP serverio ir Desktop integration statusas
- **powerbi://workspaces** - Visų Power BI workspaces sąrašas
- **powerbi://datasets** - Duomenų rinkinių sąrašas
- **powerbi://reports** - Ataskaitų sąrašas

### 📝 Prompts (Šablonai)
- **analyze_business_requirements()** - Verslo reikalavimų analizė ir Power BI architektūros rekomendacijos
- **create_dax_best_practices()** - DAX geriausių praktikų gidas su pavyzdžiais

## 🚀 Diegimas

### 1. Repository kloniranje

```bash
git clone https://github.com/roqusanalytics/power-bi-mcp.git
cd power-bi-mcp
```

### 2. Priklausomybių diegimas

```bash
# Pagrindinės priklausomybės (visos platformos)
pip install -r requirements.txt

# Arba naudojant uv
uv sync
```

### 3. Windows specialių priklausomybių diegimas (TOM integration)

```bash
# Windows aplinkoje (reikalinga real-time Desktop integration)
pip install pythonnet>=3.0.1 pywin32>=306 comtypes>=1.2.0

# Arba su uv
uv sync --extra windows
```

### 4. Environment konfigūracija

```bash
# Nukopijuoti .env failą
cp .env.example .env

# Redaguoti .env failą su savo Azure AD kredencialais
nano .env
```

## 💻 Naudojimas

### 1. Serverio paleidimas

```bash
# Tiesioginis paleidimas
python src/power_bi_mcp/server.py

# Arba su uv
uv run python src/power_bi_mcp/server.py
```

### 2. MCP Inspector testavimas

```bash
# Testuoti serverio veikimą su MCP Inspector
npx @modelcontextprotocol/inspector python src/power_bi_mcp/server.py
```

### 3. Claude Desktop konfigūracija

Pridėkite į `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "power-bi": {
      "command": "python",
      "args": [
        "path/to/power-bi-mcp/src/power_bi_mcp/server.py"
      ],
      "cwd": "path/to/power-bi-mcp",
      "env": {
        "PYTHONPATH": "path/to/power-bi-mcp/src"
      }
    }
  }
}
```

## 📋 Naudojimo pavyzdžiai

### 🎯 Real-time Desktop Integration

```text
// Prisijungti prie Power BI Desktop
Prisijunk prie Power BI Desktop real-time modelio valdymui

// Sukurti DAX measure real-time
Sukurk DAX measure "Total Sales" lentelėje "Sales" su formule SUM(Sales[Amount])

// Sukurti calculated column
Sukurk calculated column "Profit Margin" lentelėje Sales su formule DIVIDE([Profit], [Revenue], 0) 

// Sukurti table relationship
Sukurk ryšį tarp Sales[CustomerID] ir Customers[CustomerID] stulpelių

// Gauti modelio informaciją
Parodyk Power BI Desktop modelio metadata ir struktūrą
```

### 🔗 Power BI Service Integration

```text
// Prisijungti prie Power BI Service
Prisijunk prie Power BI Service su Azure AD

// Vykdyti DAX užklausą
Vykdyk DAX užklausą: EVALUATE SUMMARIZE(Sales, Products[Category], "Total", SUM(Sales[Amount]))

// Atnaujinti dataset
Atnaujink duomenų rinkinį su ID: abc123-def456-ghi789
```

### 🧮 DAX Optimization

```text
// Optimizuoti DAX formulę
Optimizuok šią DAX formulę: SUMX(FILTER(Sales, Sales[Year] = 2024), Sales[Amount])

// Generuoti Time Intelligence measures
Sugeneruok time intelligence measures rinkinį "Revenue" measure su prefiksu "Sales"
```

## 🖥️ Palaikomos platformos

### Windows (Rekomenduojama)
- ✅ **Pilnas funkcionalumas** su Power BI Desktop TOM integration
- ✅ **Real-time model modifications** per .NET Analysis Services
- ✅ **XMLA endpoint discovery** ir automatic connection 
- ✅ **External Tools registration** Power BI Desktop ribbon
- ✅ **Process detection** ir port scanning

### Linux/WSL
- ✅ **Power BI Service API** integration
- ✅ **DAX optimization tools** 
- ✅ **Business analysis** ir reporting
- ❌ **Real-time Desktop integration** (Windows only)
- ⚠️ **Simulation mode** testavimui ir plėtojimui

## 🔧 Technologijos

### TOM (Tabular Object Model) Integration
- **pythonnet** - .NET CLR integration Python aplinkoje
- **Microsoft.AnalysisServices.Tabular** - TOM API real-time model manipulation
- **XMLA Discovery** - Automatic Power BI Desktop process ir port detection
- **Cross-platform compatibility** - Graceful fallbacks when Windows-only features unavailable

### Power BI Service API
- **Azure Identity** - Azure AD authentication su Service Principal
- **REST API** - Power BI Service endpoints integration
- **XMLA endpoints** - Premium workspace connectivity
- **DAX Query execution** - Both Service ir Desktop support

## 🎯 Pagrindiniai pasiekimai

✅ **Real-time Power BI Desktop integration** per TOM API  
✅ **Automatic process discovery** ir XMLA endpoint detection  
✅ **Cross-platform compatibility** su graceful Windows/Linux fallbacks  
✅ **Comprehensive DAX tools** optimization ir best practices  
✅ **Power BI Service API integration** su Azure AD authentication  
✅ **External Tools support** Power BI Desktop ribbon integration  
✅ **Business requirements analysis** ir architectural recommendations  

## 📝 Licencija

Sukurta Claude Code Assistant projektui. Model Context Protocol (MCP) integration.

## 🤝 Palaikymas

- **MCP Documentation:** https://modelcontextprotocol.io
- **Power BI REST API:** https://docs.microsoft.com/power-bi/developer/
- **Analysis Services Documentation:** https://docs.microsoft.com/analysis-services/
- **Issues:** GitHub repository issues section