[index.html](https://github.com/user-attachments/files/29618759/index.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OUZ Group — Solicitações de Pagamento</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  body{font-family:'Poppins',sans-serif;background:#FFF8EE;color:#2C2C2A;min-height:100vh}
  .container{max-width:960px;margin:0 auto;padding:2rem 1.5rem}

  /* TOPBAR */
  .topbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem}
  .brand{font-size:18px;font-weight:700;display:flex;align-items:center;gap:10px;letter-spacing:-.3px}
  .brand-icon{width:38px;height:38px;background:#412402;border-radius:10px;display:flex;align-items:center;justify-content:center;color:#FEDDB9;font-size:18px}
  .brand-sub{font-size:11px;font-weight:400;color:#854F0B;display:block;margin-top:-2px}
  .date-chip{font-size:12px;color:#854F0B;font-weight:500;background:#FFEED0;border:1px solid #EFC99A;border-radius:20px;padding:5px 14px}

  /* KPI */
  .kpi-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem}
  .kpi{background:#FFEED0;border:1px solid #EFC99A;border-radius:10px;padding:14px 16px}
  .kpi-val{font-size:24px;font-weight:700;line-height:1.1}
  .kpi-lbl{font-size:10px;color:#854F0B;margin-top:3px;text-transform:uppercase;letter-spacing:.05em}

  /* TABS */
  .tabs{display:flex;border-bottom:1px solid #EFC99A;margin-bottom:1.5rem;gap:0;background:#fff;border-radius:12px 12px 0 0;padding:0 4px}
  .tab{flex:1;padding:12px 8px;font-size:13px;font-weight:400;cursor:pointer;border:none;background:none;color:#854F0B;border-bottom:2px solid transparent;transition:all .15s;font-family:'Poppins',sans-serif;display:flex;align-items:center;justify-content:center;gap:5px;margin-bottom:-1px}
  .tab.on{color:#412402;font-weight:600;border-bottom-color:#BA7517}
  .tab:hover{color:#412402}
  .view{display:none}.view.on{display:block}

  /* FORM */
  .form-card{background:#FFEED0;border:1px solid #EFC99A;border-radius:12px;padding:1.25rem;margin-bottom:1.25rem}
  .sect-hd{font-size:11px;font-weight:600;color:#854F0B;text-transform:uppercase;letter-spacing:.08em;margin-bottom:14px;display:flex;align-items:center;gap:6px}
  .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .form-grid-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
  .form-grid-full{grid-column:span 2}
  .field{display:flex;flex-direction:column;gap:4px}
  .field label{font-size:11px;font-weight:600;color:#633806;text-transform:uppercase;letter-spacing:.05em}
  .field input,.field select{width:100%;font-family:'Poppins',sans-serif;background:#fff;border:1px solid #EFC99A;border-radius:8px;height:38px;padding:0 12px;font-size:13px;color:#2C2C2A;outline:none;transition:border-color .15s}
  .field input:focus,.field select:focus{border-color:#BA7517;box-shadow:0 0 0 3px rgba(186,117,23,.1)}
  .field textarea{width:100%;font-family:'Poppins',sans-serif;background:#fff;border:1px solid #EFC99A;border-radius:8px;padding:8px 12px;font-size:13px;resize:none;height:62px;color:#2C2C2A;outline:none;transition:border-color .15s}
  .field textarea:focus{border-color:#BA7517;box-shadow:0 0 0 3px rgba(186,117,23,.1)}

  /* UPLOAD */
  .upload-area{background:#fff;border:2px dashed #EFC99A;border-radius:10px;padding:16px;text-align:center;cursor:pointer;transition:all .2s;position:relative}
  .upload-area:hover,.upload-area.drag{border-color:#BA7517;background:#FFFBF5}
  .upload-area input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
  .upload-area .up-icon{font-size:24px;color:#EFC99A;margin-bottom:4px}
  .upload-area .up-txt{font-size:12px;color:#854F0B;font-weight:500}
  .upload-area .up-sub{font-size:11px;color:#A87840;margin-top:2px}
  .file-list{margin-top:8px;display:flex;flex-direction:column;gap:5px}
  .file-item{display:flex;align-items:center;gap:8px;background:#FFEED0;border:1px solid #EFC99A;border-radius:8px;padding:6px 10px;font-size:12px}
  .file-item .fi-name{flex:1;min-width:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color:#412402;font-weight:500}
  .file-item .fi-size{color:#854F0B;flex-shrink:0}
  .file-item .fi-del{background:none;border:none;cursor:pointer;color:#A32D2D;font-size:14px;padding:0;flex-shrink:0;display:flex;align-items:center}

  /* PRIO */
  .prio-row{display:flex;gap:8px}
  .prio-opt{flex:1;position:relative}
  .prio-opt input[type=radio]{position:absolute;opacity:0;width:0;height:0}
  .prio-opt label{display:flex;align-items:center;justify-content:center;gap:6px;padding:9px 12px;border-radius:8px;border:2px solid #EFC99A;cursor:pointer;font-size:13px;font-weight:500;transition:all .15s;background:#fff;color:#854F0B}
  .prio-opt input:checked+label.normal-lbl{border-color:#3B6D11;background:#EAF3DE;color:#27500A}
  .prio-opt input:checked+label.urgent-lbl{border-color:#B83232;background:#FCEBEB;color:#791F1F}

  /* BOTÕES */
  .btn-primary{background:#412402;color:#FEDDB9;border:none;border-radius:8px;padding:10px 22px;font-size:13px;font-weight:600;cursor:pointer;display:inline-flex;align-items:center;gap:7px;transition:all .15s;font-family:'Poppins',sans-serif}
  .btn-primary:hover{background:#633806}
  .btn-add{background:#FEDDB9;color:#412402;border:1px solid #EFC99A;border-radius:8px;padding:9px 20px;font-size:13px;font-weight:600;cursor:pointer;display:inline-flex;align-items:center;gap:6px;transition:all .15s;font-family:'Poppins',sans-serif}
  .btn-add:hover{background:#f5c990}

  /* FILTROS */
  .filter-bar{display:flex;gap:8px;margin-bottom:1rem;flex-wrap:wrap;align-items:center}
  .filter-lbl{font-size:11px;color:#854F0B;font-weight:500}
  .filter-chip{font-size:11px;font-weight:500;padding:4px 12px;border-radius:20px;border:1px solid #EFC99A;background:#fff;cursor:pointer;color:#854F0B;transition:all .15s;font-family:'Poppins',sans-serif}
  .filter-chip.on{border-color:#BA7517;color:#412402;background:#FEDDB9}
  .filter-chip:hover{background:#FFEED0}

  /* CARDS DE SOLICITAÇÃO */
  .task-list{display:flex;flex-direction:column;gap:6px}
  .empty-state{text-align:center;padding:3rem;color:#888780;font-size:14px}
  .empty-state i{font-size:36px;display:block;margin-bottom:10px;color:#EFC99A}
  .date-divider{font-size:11px;font-weight:600;color:#854F0B;margin:14px 0 8px;display:flex;align-items:center;gap:6px}
  .task-item{background:#fff;border:1px solid #EFC99A;border-radius:12px;padding:14px 16px;display:flex;align-items:flex-start;gap:12px;transition:border-color .15s}
  .task-item:hover{border-color:#BA7517}
  .task-item.done-item{opacity:.55}
  .chk{width:22px;height:22px;border-radius:50%;border:2px solid #EFC99A;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:2px;transition:all .15s;color:#fff;font-size:11px;background:#fff}
  .chk.on{background:#3B6D11;border-color:#3B6D11}
  .task-body{flex:1;min-width:0}
  .task-name{font-size:14px;font-weight:600}
  .task-name.struck{text-decoration:line-through;color:#888780;font-weight:400}
  .task-meta{display:flex;align-items:center;gap:8px;margin-top:5px;flex-wrap:wrap}
  .task-time{font-size:12px;color:#5F5E5A;display:flex;align-items:center;gap:3px}
  .task-note{font-size:12px;color:#888780;margin-top:4px}
  .pill{font-size:11px;padding:2px 9px;border-radius:20px;font-weight:500;white-space:nowrap}
  .btn-del{background:none;border:1px solid #F7C1C1;border-radius:8px;padding:3px 8px;cursor:pointer;color:#A32D2D;font-size:13px;transition:all .15s;flex-shrink:0;margin-top:1px}
  .btn-del:hover{background:#FCEBEB}
  .attach-badge{font-size:11px;color:#185FA5;display:flex;align-items:center;gap:3px;margin-top:3px}

  /* KANBAN */
  .kb-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
  .kb-col{background:#FFEED0;border:1px solid #EFC99A;border-radius:12px;padding:14px;min-height:200px}
  .kb-col-hd{font-size:12px;font-weight:600;color:#412402;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between}
  .kb-badge{font-size:11px;background:#FEDDB9;color:#633806;border-radius:20px;padding:1px 9px;font-weight:500;border:1px solid #EFC99A}
  .kb-card{background:#fff;border:1px solid #EFC99A;border-radius:10px;padding:12px 13px;margin-bottom:7px}
  .kb-card-name{font-size:13px;font-weight:600;margin-bottom:6px}
  .kb-card-meta{display:flex;align-items:center;gap:5px;flex-wrap:wrap;margin-bottom:8px}
  .kb-actions{display:flex;gap:5px;justify-content:flex-end}
  .kb-mv{font-size:11px;border:1px solid #EFC99A;border-radius:8px;padding:3px 9px;background:#fff;cursor:pointer;color:#854F0B;font-family:'Poppins',sans-serif;transition:all .15s}
  .kb-mv:hover{background:#FEDDB9}
  .kb-empty{font-size:12px;color:#888780;text-align:center;padding:20px 8px}

  /* DASHBOARD */
  .dash-grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px}
  .dc{background:#fff;border:1px solid #EFC99A;border-radius:12px;padding:1.25rem}
  .dc-title{font-size:11px;font-weight:600;color:#854F0B;text-transform:uppercase;letter-spacing:.06em;margin-bottom:1rem}
  .prog-row{margin-bottom:10px}
  .prog-hd{display:flex;justify-content:space-between;font-size:12px;margin-bottom:4px}
  .prog-track{height:6px;background:#FFEED0;border-radius:3px;overflow:hidden;border:1px solid #EFC99A}
  .prog-fill{height:100%;border-radius:3px;transition:width .4s}

  /* TOAST */
  .toast{position:fixed;bottom:24px;right:24px;background:#412402;color:#FEDDB9;font-family:'Poppins',sans-serif;font-size:13px;padding:10px 18px;border-radius:10px;opacity:0;transition:opacity .3s;pointer-events:none;z-index:999;display:flex;align-items:center;gap:8px}
  .toast.show{opacity:1}

  /* EMAIL MODAL */
  .modal-overlay{position:fixed;inset:0;background:rgba(44,44,42,.45);z-index:100;display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .2s}
  .modal-overlay.show{opacity:1;pointer-events:all}
  .modal{background:#fff;border:1px solid #EFC99A;border-radius:16px;padding:1.75rem;max-width:480px;width:90%;box-shadow:0 20px 60px rgba(0,0,0,.12);transform:translateY(16px);transition:transform .2s}
  .modal-overlay.show .modal{transform:translateY(0)}
  .modal-title{font-size:16px;font-weight:700;color:#412402;margin-bottom:4px}
  .modal-sub{font-size:13px;color:#854F0B;margin-bottom:1.25rem}
  .modal-body{font-size:13px;color:#2C2C2A;line-height:1.6;background:#FFEED0;border:1px solid #EFC99A;border-radius:10px;padding:14px;margin-bottom:1.25rem;white-space:pre-wrap}
  .modal-footer{display:flex;gap:8px;justify-content:flex-end}
  .btn-cancel{background:#fff;color:#854F0B;border:1px solid #EFC99A;border-radius:8px;padding:9px 18px;font-size:13px;font-weight:500;cursor:pointer;font-family:'Poppins',sans-serif;transition:all .15s}
  .btn-cancel:hover{background:#FFEED0}

  @media(max-width:640px){
    .kpi-row{grid-template-columns:1fr 1fr}
    .form-grid{grid-template-columns:1fr}
    .form-grid-full{grid-column:span 1}
    .form-grid-3{grid-template-columns:1fr 1fr}
    .kb-grid{grid-template-columns:1fr}
    .dash-grid2{grid-template-columns:1fr}
    .tabs .tab span.tab-label{display:none}
  }
</style>
</head>
<body>
<div class="container">

  <div class="topbar">
    <div class="brand">
      <div class="brand-icon"><i class="ti ti-receipt"></i></div>
      <div>
        OUZ Group
        <span class="brand-sub">Solicitações de Pagamento</span>
      </div>
    </div>
    <div style="display:flex;align-items:center;gap:8px">
      <button onclick="load()" title="Sincronizar com Google Sheets" style="background:#FEDDB9;color:#412402;border:1px solid #EFC99A;border-radius:8px;padding:6px 12px;font-size:12px;font-weight:600;cursor:pointer;display:inline-flex;align-items:center;gap:5px;font-family:Poppins,sans-serif;transition:all .15s" onmouseover="this.style.background='#f5c990'" onmouseout="this.style.background='#FEDDB9'"><i class="ti ti-refresh" style="font-size:14px"></i> Sincronizar</button>
      <div class="date-chip" id="date-display"></div>
    </div>
  </div>

  <div class="kpi-row">
    <div class="kpi"><div class="kpi-val" id="k-total" style="color:#412402">0</div><div class="kpi-lbl">Solicitações</div></div>
    <div class="kpi"><div class="kpi-val" id="k-pago" style="color:#3B6D11">0</div><div class="kpi-lbl">Pagas</div></div>
    <div class="kpi"><div class="kpi-val" id="k-urgente" style="color:#B83232">0</div><div class="kpi-lbl">Urgentes</div></div>
    <div class="kpi"><div class="kpi-val" id="k-setores" style="color:#534AB7">0</div><div class="kpi-lbl">Setores ativos</div></div>
  </div>

  <div class="tabs">
    <button class="tab on" onclick="sw('agenda',this)"><i class="ti ti-file-invoice"></i> <span class="tab-label">Solicitações</span></button>
    <button class="tab" onclick="sw('kanban',this)"><i class="ti ti-layout-columns"></i> <span class="tab-label">Kanban</span></button>
    <button class="tab" onclick="sw('dash',this)"><i class="ti ti-chart-bar"></i> <span class="tab-label">Dashboard</span></button>
  </div>

  <!-- SOLICITAÇÕES -->
  <div class="view on" id="v-agenda">
    <div class="form-card">
      <div class="sect-hd"><i class="ti ti-plus-circle" style="font-size:15px"></i> Nova Solicitação</div>

      <div class="form-grid" style="margin-bottom:10px">
        <div class="field form-grid-full">
          <label>Nome da Solicitação</label>
          <input type="text" id="f-nome" placeholder="Ex: Pagamento fornecedor materiais" />
        </div>
        <div class="field form-grid-full">
          <label>Responsável pela Solicitação</label>
          <input type="text" id="f-responsavel" placeholder="Ex: João Silva" />
        </div>
      </div>

      <div class="form-grid-3" style="margin-bottom:10px">
        <div class="field">
          <label>Data da Solicitação</label>
          <input type="date" id="f-data" />
        </div>
        <div class="field">
          <label>Data do Pagamento</label>
          <input type="date" id="f-datapgto" />
        </div>
        <div class="field">
          <label>Número da NF</label>
          <input type="text" id="f-nf" placeholder="Ex: 001234" />
        </div>
      </div>

      <div class="form-grid" style="margin-bottom:10px">
        <div class="field">
          <label>Setor / Centro de Custo</label>
          <select id="f-setor">
            <option value="Custo Raso Obra">Custo Raso Obra</option>
            <option value="Custo Indireto Obra">Custo Indireto Obra</option>
            <option value="Projetos">Projetos</option>
            <option value="OUZ">OUZ</option>
            <option value="Pos Obra">Pós Obra</option>
            <option value="Outros">Outros</option>
            <option value="Reembolso">Reembolso</option>
          </select>
        </div>
        <div class="field">
          <label>Prioridade</label>
          <div class="prio-row">
            <div class="prio-opt">
              <input type="radio" name="prio" id="prio-normal" value="normal" checked>
              <label for="prio-normal" class="normal-lbl"><i class="ti ti-circle-check" style="font-size:14px"></i> Normal</label>
            </div>
            <div class="prio-opt">
              <input type="radio" name="prio" id="prio-urgente" value="urgente">
              <label for="prio-urgente" class="urgent-lbl"><i class="ti ti-alert-triangle" style="font-size:14px"></i> Urgente</label>
            </div>
          </div>
        </div>
      </div>

      <div style="background:#FFF4E8;margin-bottom:10px;padding:1rem;border:1px solid #EFC99A;border-radius:10px">
        <div class="sect-hd" style="margin-bottom:12px"><i class="ti ti-building-bank" style="font-size:15px"></i> Dados para Pagamento</div>
        <div class="form-grid" style="margin-bottom:10px">
          <div class="field">
            <label>Forma de Pagamento</label>
            <select id="f-forma">
              <option value="">Selecione...</option>
              <option value="PIX">PIX</option>
              <option value="TED/DOC">TED / DOC</option>
              <option value="Boleto">Boleto</option>
            </select>
          </div>
          <div class="field">
            <label>CNPJ / CPF</label>
            <input type="text" id="f-cnpj" placeholder="Ex: 00.000.000/0001-00" />
          </div>
        </div>
        <div class="form-grid-3" style="margin-bottom:10px">
          <div class="field">
            <label>Banco</label>
            <input type="text" id="f-banco" placeholder="Ex: Bradesco" />
          </div>
          <div class="field">
            <label>Agência</label>
            <input type="text" id="f-agencia" placeholder="Ex: 1234-5" />
          </div>
          <div class="field">
            <label>Conta</label>
            <input type="text" id="f-conta" placeholder="Ex: 12345-6" />
          </div>
        </div>
        <div class="field">
          <label>Chave PIX</label>
          <input type="text" id="f-pix" placeholder="E-mail, CPF, CNPJ ou chave aleatória" />
        </div>
      </div>

      <div class="field" style="margin-bottom:10px;margin-top:10px">
        <label>Observação (opcional)</label>
        <textarea id="f-obs" placeholder="Detalhes adicionais, fornecedor, descrição do serviço..."></textarea>
      </div>

      <div class="field" style="margin-bottom:16px">
        <label>Anexos</label>
        <div class="upload-area" id="upload-area">
          <input type="file" id="f-files" multiple accept=".pdf,.jpg,.jpeg,.png,.xlsx,.xls,.doc,.docx" onchange="handleFiles(this.files)">
          <div class="up-icon"><i class="ti ti-cloud-upload"></i></div>
          <div class="up-txt">Clique ou arraste arquivos aqui</div>
          <div class="up-sub">PDF, imagens, planilhas e documentos • máx. 5MB por arquivo</div>
        </div>
        <div class="file-list" id="file-list"></div>
      </div>

      <div style="display:flex;gap:10px;flex-wrap:wrap">
        <button class="btn-primary" onclick="addTask()"><i class="ti ti-send"></i> Enviar Solicitação</button>
        <button class="btn-add" onclick="clearForm()"><i class="ti ti-refresh"></i> Limpar</button>
      </div>
    </div>

    <div class="filter-bar">
      <span class="filter-lbl">Filtrar:</span>
      <button class="filter-chip on" onclick="setFilter('todos',this)">Todos</button>
      <button class="filter-chip" onclick="setFilter('hoje',this)">Hoje</button>
      <button class="filter-chip" onclick="setFilter('urgentes',this)">Urgentes</button>
      <button class="filter-chip" onclick="setFilter('pendentes',this)">Pendentes</button>
      <button class="filter-chip" onclick="setFilter('pagos',this)">Pagos</button>
    </div>
    <div class="task-list" id="task-list"></div>
  </div>

  <!-- KANBAN -->
  <div class="view" id="v-kanban">
    <div class="kb-grid">
      <div class="kb-col">
        <div class="kb-col-hd"><span><i class="ti ti-circle"></i> Aguardando</span><span class="kb-badge" id="kb-cnt-todo">0</span></div>
        <div id="kb-todo"></div>
      </div>
      <div class="kb-col">
        <div class="kb-col-hd"><span><i class="ti ti-clock"></i> Em Análise</span><span class="kb-badge" id="kb-cnt-doing">0</span></div>
        <div id="kb-doing"></div>
      </div>
      <div class="kb-col">
        <div class="kb-col-hd"><span><i class="ti ti-circle-check"></i> Pago</span><span class="kb-badge" id="kb-cnt-done">0</span></div>
        <div id="kb-done"></div>
      </div>
    </div>
  </div>

  <!-- DASHBOARD -->
  <div class="view" id="v-dash">
    <div class="kpi-row" style="margin-bottom:1.25rem">
      <div class="kpi"><div class="kpi-val" id="d-taxa" style="color:#3B6D11">—</div><div class="kpi-lbl">% Pagas</div></div>
      <div class="kpi"><div class="kpi-val" id="d-urg" style="color:#B83232">0</div><div class="kpi-lbl">Urgentes Pend.</div></div>
      <div class="kpi"><div class="kpi-val" id="d-pend" style="color:#534AB7">0</div><div class="kpi-lbl">Pendentes</div></div>
      <div class="kpi"><div class="kpi-val" id="d-setcount" style="color:#BA7517">0</div><div class="kpi-lbl">Setores</div></div>
    </div>
    <div class="dc" style="margin-bottom:12px">
      <div class="dc-title">Prioridade — Normal vs Urgente</div>
      <div style="display:flex;align-items:center;gap:16px;flex-wrap:wrap">
        <div style="flex:1;min-width:160px">
          <div class="prog-row" style="margin-bottom:12px">
            <div class="prog-hd"><span style="color:#27500A;font-weight:600"><i class="ti ti-circle-check" style="font-size:12px"></i> Normal</span><span id="d-prio-normal-lbl" style="color:#888780">0 (—)</span></div>
            <div class="prog-track"><div class="prog-fill" id="d-prio-normal-bar" style="width:0%;background:#3B6D11"></div></div>
          </div>
          <div class="prog-row">
            <div class="prog-hd"><span style="color:#791F1F;font-weight:600"><i class="ti ti-alert-triangle" style="font-size:12px"></i> Urgente</span><span id="d-prio-urgente-lbl" style="color:#888780">0 (—)</span></div>
            <div class="prog-track"><div class="prog-fill" id="d-prio-urgente-bar" style="width:0%;background:#B83232"></div></div>
          </div>
        </div>
        <div style="position:relative;width:120px;height:120px;flex-shrink:0"><canvas id="chart-prio"></canvas></div>
      </div>
    </div>
    <div class="dash-grid2">
      <div class="dc"><div class="dc-title">Solicitações por setor</div><div id="d-setor-bars"></div></div>
      <div class="dc"><div class="dc-title">Status por setor</div><div id="d-setor-done"></div></div>
    </div>
    <div class="dc" style="margin-bottom:12px">
      <div class="dc-title">Distribuição por centro de custo</div>
      <div style="position:relative;width:100%;height:200px"><canvas id="chart-pie"></canvas></div>
      <div id="pie-legend" style="display:flex;flex-wrap:wrap;gap:8px 16px;margin-top:12px"></div>
    </div>
    <div class="dc">
      <div class="dc-title">Solicitações — últimos 7 dias</div>
      <div style="position:relative;width:100%;height:170px"><canvas id="chart-dia"></canvas></div>
    </div>
  </div>

</div>

<!-- MODAL EMAIL -->
<div class="modal-overlay" id="email-modal">
  <div class="modal">
    <div class="modal-title"><i class="ti ti-mail"></i> Confirmar Envio</div>
    <div class="modal-sub">Um e-mail será enviado para o Financeiro com os detalhes abaixo:</div>
    <div class="modal-body" id="modal-body-text"></div>
    <div class="modal-footer">
      <button class="btn-cancel" onclick="closeModal()">Cancelar</button>
      <button class="btn-primary" onclick="confirmSend()"><i class="ti ti-send"></i> Confirmar e Enviar</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"><i class="ti ti-check"></i> <span id="toast-msg"></span></div>

<script>
const SETOR_COLORS={
  'Custo Raso Obra':'#D85A30',
  'Custo Indireto Obra':'#D4537E',
  'Projetos':'#1D9E75',
  'OUZ':'#7F77DD',
  'Pos Obra':'#378ADD',
  'Outros':'#888780',
  'Reembolso':'#BA7517'
};
const SETOR_BG={
  'Custo Raso Obra':'#FAECE7',
  'Custo Indireto Obra':'#FBEAF0',
  'Projetos':'#E1F5EE',
  'OUZ':'#EEEDFE',
  'Pos Obra':'#E6F1FB',
  'Outros':'#F0F0EF',
  'Reembolso':'#FFEED0'
};
const SETOR_TXT={
  'Custo Raso Obra':'#712B13',
  'Custo Indireto Obra':'#72243E',
  'Projetos':'#085041',
  'OUZ':'#3C3489',
  'Pos Obra':'#0C447C',
  'Outros':'#4A4A48',
  'Reembolso':'#633806'
};
const KB_STATUS=['todo','doing','done'];
const MAX_FILE_MB=5;
const GAS_URL='https://script.google.com/macros/s/AKfycbwWrGYl18IGpvdsaBK7tiDrttJ97e3oSk6mNMnG7MFJW62dJo0KLgNIgDk00th0MZvjBA/exec';

let nid=1, tasks=[], activeFilter='todos', pendingTask=null;

// --- PERSISTÊNCIA (Google Sheets) ---
async function save(){
  try{
    localStorage.setItem('ouz_backup', JSON.stringify({nid, tasks}));
    const url=GAS_URL+'?action=save&nid='+nid+'&tasks='+encodeURIComponent(JSON.stringify(tasks));
    await fetch(url,{method:'GET',mode:'no-cors'});
  } catch(e){showToast('\u26a0 Erro ao salvar. Verifique sua conexão.')}
}

async function load(){
  setLoading(true);
  const timeout=new Promise((_,rej)=>setTimeout(()=>rej(new Error('timeout')),8000));
  try{
    const res=await Promise.race([fetch(GAS_URL+'?action=get'),timeout]);
    const json=await res.json();
    if(json.ok){nid=json.data.nid||1;tasks=json.data.tasks||[];}
    showToast('✓ Dados sincronizados!');
  } catch(e){
    showToast('⚠ Sem conexão — exibindo dados locais.');
    try{const raw=localStorage.getItem('ouz_backup');if(raw){const d=JSON.parse(raw);nid=d.nid||1;tasks=d.tasks||[];}}catch(e2){}
  } finally{setLoading(false);render();}
}

function setLoading(on){
  let el=document.getElementById('loading-bar');
  if(!el){
    el=document.createElement('div');el.id='loading-bar';
    el.style.cssText='position:fixed;top:0;left:0;width:100%;height:3px;background:#BA7517;z-index:9999;transition:opacity .4s';
    document.body.appendChild(el);
  }
  el.style.opacity=on?'1':'0';
}

function showToast(msg){
  document.getElementById('toast-msg').textContent=msg;
  const t=document.getElementById('toast');t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2800);
}

// --- UPLOAD (base64) ---
let currentFiles=[]; // [{name, size, type, data(base64)}]

function handleFiles(fileList){
  const incoming=Array.from(fileList);
  let skipped=0;
  const promises=incoming.map(f=>{
    if(f.size>MAX_FILE_MB*1024*1024){skipped++;return Promise.resolve(null)}
    if(currentFiles.find(x=>x.name===f.name&&x.size===f.size))return Promise.resolve(null);
    return new Promise(res=>{
      const r=new FileReader();
      r.onload=e=>res({name:f.name,size:f.size,type:f.type,data:e.target.result});
      r.readAsDataURL(f);
    });
  });
  Promise.all(promises).then(results=>{
    results.forEach(r=>{if(r)currentFiles.push(r)});
    if(skipped)showToast(`⚠ ${skipped} arquivo(s) ignorado(s): tamanho acima de ${MAX_FILE_MB}MB`);
    renderFileList();
  });
}
function renderFileList(){
  const el=document.getElementById('file-list');
  if(!currentFiles.length){el.innerHTML='';return}
  el.innerHTML=currentFiles.map((f,i)=>`
    <div class="file-item">
      <i class="ti ti-paperclip" style="color:#854F0B;font-size:14px;flex-shrink:0"></i>
      <span class="fi-name">${f.name}</span>
      <span class="fi-size">${formatFileSize(f.size)}</span>
      <button class="fi-del" onclick="removeFile(${i})" title="Remover"><i class="ti ti-x"></i></button>
    </div>`).join('');
}
function removeFile(i){currentFiles.splice(i,1);renderFileList()}
function formatFileSize(b){if(b<1024)return b+'B';if(b<1048576)return Math.round(b/1024)+'KB';return(b/1048576).toFixed(1)+'MB'}

function downloadFile(taskId,fileIdx){
  const t=tasks.find(x=>x.id===taskId);
  if(!t||!t.files||!t.files[fileIdx])return;
  const f=t.files[fileIdx];
  const a=document.createElement('a');
  a.href=f.data;a.download=f.name;a.click();
}

// drag & drop
const ua=document.getElementById('upload-area');
['dragenter','dragover'].forEach(ev=>ua.addEventListener(ev,e=>{e.preventDefault();ua.classList.add('drag')}));
['dragleave','drop'].forEach(ev=>ua.addEventListener(ev,e=>{e.preventDefault();ua.classList.remove('drag')}));
ua.addEventListener('drop',e=>{if(e.dataTransfer.files.length)handleFiles(e.dataTransfer.files)});

// --- HELPERS ---
function todayStr(){return new Date().toISOString().slice(0,10)}
function fmtDateBR(s){if(!s)return'—';const[y,m,d]=s.split('-');return`${d}/${m}/${y}`}
function pillHtml(s){return`<span class="pill" style="background:${SETOR_BG[s]||'#FFEED0'};color:${SETOR_TXT[s]||'#633806'}">${s}</span>`}

// --- NAVEGAÇÃO ---
function sw(v,btn){
  document.querySelectorAll('.view').forEach(e=>e.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(e=>e.classList.remove('on'));
  document.getElementById('v-'+v).classList.add('on');btn.classList.add('on');render();
}
function setFilter(f,btn){
  activeFilter=f;
  document.querySelectorAll('.filter-chip').forEach(e=>e.classList.remove('on'));
  btn.classList.add('on');renderAgenda();
}

// --- FORM ---
function clearForm(){
  document.getElementById('f-nome').value='';
  document.getElementById('f-responsavel').value='';
  document.getElementById('f-datapgto').value='';
  document.getElementById('f-nf').value='';
  document.getElementById('f-forma').value='';
  document.getElementById('f-cnpj').value='';
  document.getElementById('f-banco').value='';
  document.getElementById('f-agencia').value='';
  document.getElementById('f-conta').value='';
  document.getElementById('f-pix').value='';
  document.getElementById('f-obs').value='';
  document.getElementById('f-data').value=todayStr();
  document.getElementById('prio-normal').checked=true;
  currentFiles=[];renderFileList();
  document.getElementById('f-files').value='';
}

// --- ADD TASK ---
function addTask(){
  const nome=document.getElementById('f-nome').value.trim();
  if(!nome){document.getElementById('f-nome').focus();showToast('⚠ Preencha o nome da solicitação');return}
  const responsavel=document.getElementById('f-responsavel').value.trim();
  const dataSolic=document.getElementById('f-data').value||todayStr();
  const dataPgto=document.getElementById('f-datapgto').value;
  const nf=document.getElementById('f-nf').value.trim();
  const setor=document.getElementById('f-setor').value;
  const prio=document.querySelector('input[name="prio"]:checked').value;
  const obs=document.getElementById('f-obs').value.trim();
  const forma=document.getElementById('f-forma').value;
  const cnpj=document.getElementById('f-cnpj').value.trim();
  const banco=document.getElementById('f-banco').value.trim();
  const agencia=document.getElementById('f-agencia').value.trim();
  const conta=document.getElementById('f-conta').value.trim();
  const pix=document.getElementById('f-pix').value.trim();
  const files=[...currentFiles]; // array com {name,size,type,data}
  const fileNames=files.map(f=>f.name);

  pendingTask={
    id:nid++,nome,responsavel,
    data:dataSolic,
    dataPgto:dataPgto||'',
    nf:nf||'',
    setor,prio,obs,
    forma,cnpj,banco,agencia,conta,pix,
    files,
    fileNames,
    kbStatus:'todo',done:false,
    createdAt:new Date().toISOString()
  };

  // Montar preview do email
  const emailBody=buildEmailBody(pendingTask);
  document.getElementById('modal-body-text').textContent=emailBody;
  document.getElementById('email-modal').classList.add('show');
}

function buildEmailBody(t){
  return [
    `NOVA SOLICITAÇÃO DE PAGAMENTO`,
    ``,
    `Nome: ${t.nome}`,
    `Responsável: ${t.responsavel||'Não informado'}`,
    `Data da Solicitação: ${fmtDateBR(t.data)}`,
    `Data do Pagamento: ${t.dataPgto?fmtDateBR(t.dataPgto):'Não informada'}`,
    `Número da NF: ${t.nf||'Não informado'}`,
    `Setor / Centro de Custo: ${t.setor}`,
    `Prioridade: ${t.prio==='urgente'?'⚠ URGENTE':'Normal'}`,
    ``,
    `--- Dados para Pagamento ---`,
    t.forma?`Forma de Pagamento: ${t.forma}`:'',
    t.cnpj?`CNPJ/CPF: ${t.cnpj}`:'',
    t.banco?`Banco: ${t.banco}`:'',
    t.agencia?`Agência: ${t.agencia}`:'',
    t.conta?`Conta: ${t.conta}`:'',
    t.pix?`Chave PIX: ${t.pix}`:'',
    ``,
    t.obs?`Observação: ${t.obs}`:'',
    t.fileNames.length?`Anexos (${t.fileNames.length}): ${t.fileNames.join(', ')}`:'',
    ``,
    `Enviado pelo sistema OUZ Group — Solicitações de Pagamento`
  ].filter(l=>l!==undefined&&!(l===''&&false)).join('\n');
}

function closeModal(){
  document.getElementById('email-modal').classList.remove('show');
  pendingTask=null;
}

async function confirmSend(){
  if(!pendingTask)return;
  tasks.push(pendingTask);
  sendEmail(pendingTask);
  clearForm();
  pendingTask=null;
  document.getElementById('email-modal').classList.remove('show');
  showToast('⏳ Salvando no Google Sheets...');
  await save();render();
  showToast('✓ Solicitação enviada ao Financeiro!');
}

// --- EMAIL VIA MAILTO ---
function sendEmail(t){
  const subject=encodeURIComponent(`[Solicitação de Pagamento] ${t.nome} — ${t.setor}${t.prio==='urgente'?' [URGENTE]':''}`);
  const body=encodeURIComponent(buildEmailBody(t));
  const mailto=`mailto:financeiro@ouzgroup.com.br?subject=${subject}&body=${body}`;
  window.open(mailto,'_blank');
}

// --- DELETE ---
async function del(id){
  if(!confirm('Remover esta solicitação?'))return;
  tasks=tasks.filter(x=>x.id!==id);
  await save();render();showToast('Solicitação removida.');
}

// --- TOGGLE PAGO ---
async function toggle(id){
  const t=tasks.find(x=>x.id===id);if(!t)return;
  t.done=!t.done;t.kbStatus=t.done?'done':t.kbStatus==='done'?'todo':t.kbStatus;
  await save();render();
}

// --- KANBAN MOVER ---
async function mvKb(id,dir){
  const t=tasks.find(x=>x.id===id);if(!t)return;
  const i=KB_STATUS.indexOf(t.kbStatus);const ni=i+dir;
  if(ni<0||ni>2)return;
  t.kbStatus=KB_STATUS[ni];t.done=t.kbStatus==='done';
  await save();render();
}

// --- FILTRO ---
function filteredTasks(){
  const today=todayStr();
  if(activeFilter==='hoje')return tasks.filter(t=>t.data===today);
  if(activeFilter==='urgentes')return tasks.filter(t=>t.prio==='urgente');
  if(activeFilter==='pendentes')return tasks.filter(t=>!t.done);
  if(activeFilter==='pagos')return tasks.filter(t=>t.done);
  return tasks;
}

// --- KPIs ---
function updateKPIs(){
  document.getElementById('k-total').textContent=tasks.length;
  document.getElementById('k-pago').textContent=tasks.filter(t=>t.done).length;
  document.getElementById('k-urgente').textContent=tasks.filter(t=>t.prio==='urgente'&&!t.done).length;
  document.getElementById('k-setores').textContent=new Set(tasks.map(t=>t.setor)).size||0;
}

// --- RENDER AGENDA ---
function renderAgenda(){
  const list=filteredTasks().slice().sort((a,b)=>a.data>b.data?1:-1);
  if(!list.length){
    document.getElementById('task-list').innerHTML=`<div class="empty-state"><i class="ti ti-receipt-off"></i>Nenhuma solicitação aqui.<br>Crie sua primeira solicitação acima!</div>`;return;
  }
  let lastDate='',html='';
  list.forEach(t=>{
    if(t.data!==lastDate){
      const isToday=t.data===todayStr();
      html+=`<div class="date-divider"><i class="ti ti-calendar"></i>${fmtDateBR(t.data)}${isToday?' &nbsp;·&nbsp; <span style="color:#3B6D11">hoje</span>':''}</div>`;
      lastDate=t.data;
    }
    const urgBg=t.prio==='urgente'?'#FCEBEB':'#FFEED0';
    const urgTxt=t.prio==='urgente'?'#791F1F':'#633806';
    const urgLbl=t.prio==='urgente'?'⚠ Urgente':'Normal';
    html+=`<div class="task-item ${t.done?'done-item':''}">
      <div class="chk ${t.done?'on':''}" onclick="toggle(${t.id})" title="${t.done?'Marcar como pendente':'Marcar como pago'}">${t.done?'<i class="ti ti-check" style="font-size:11px"></i>':''}</div>
      <div class="task-body">
        <div class="task-name ${t.done?'struck':''}">${t.nome}</div>
        <div class="task-meta">
          ${pillHtml(t.setor)}
          <span class="pill" style="background:${urgBg};color:${urgTxt}">${urgLbl}</span>
          ${t.nf?`<span class="task-time"><i class="ti ti-file-text" style="font-size:12px"></i>NF ${t.nf}</span>`:''}
          ${t.dataPgto?`<span class="task-time"><i class="ti ti-calendar-due" style="font-size:12px"></i>Pgto: ${fmtDateBR(t.dataPgto)}</span>`:''}
        </div>
        ${t.obs?'<div class="task-note">'+t.obs+'</div>':''}
        ${t.responsavel?'<div class="task-note"><i class="ti ti-user" style="font-size:11px"></i> '+t.responsavel+'</div>':''}
        ${(t.forma||t.pix||t.banco||t.cnpj)?function(){
          let p='<div class="task-note" style="display:flex;flex-wrap:wrap;gap:6px;margin-top:4px">';
          if(t.forma)p+='<span style="font-size:11px;background:#E6F1FB;color:#0C447C;border:1px solid #B8D4EF;border-radius:5px;padding:2px 7px;font-weight:500"><i class="ti ti-building-bank" style="font-size:11px"></i> '+t.forma+'</span>';
          if(t.pix)p+='<span style="font-size:11px;color:#5F5E5A"><i class="ti ti-key" style="font-size:11px"></i> PIX: '+t.pix+'</span>';
          if(t.banco)p+='<span style="font-size:11px;color:#5F5E5A">'+t.banco+(t.agencia?' | Ag: '+t.agencia:'')+(t.conta?' | Cc: '+t.conta:'')+'</span>';
          if(t.cnpj)p+='<span style="font-size:11px;color:#5F5E5A">CNPJ: '+t.cnpj+'</span>';
          return p+'</div>';
        }():''}
        ${t.files&&t.files.length?`<div class="attach-badge" style="flex-direction:column;align-items:flex-start;gap:3px">
          <span><i class="ti ti-paperclip" style="font-size:12px"></i> ${t.files.length} anexo${t.files.length>1?'s':''}</span>
          <div style="display:flex;flex-wrap:wrap;gap:4px;margin-top:2px">${t.files.map((f,fi)=>`<button onclick="downloadFile(${t.id},${fi})" style="font-size:11px;font-family:Poppins,sans-serif;background:#E6F1FB;color:#0C447C;border:1px solid #B8D4EF;border-radius:6px;padding:2px 8px;cursor:pointer;display:inline-flex;align-items:center;gap:3px;transition:background .15s" onmouseover="this.style.background='#CBE3F7'" onmouseout="this.style.background='#E6F1FB'"><i class="ti ti-download" style="font-size:11px"></i>${f.name}</button>`).join('')}</div>
        </div>`:''}
      </div>
      <button class="btn-del" onclick="del(${t.id})" title="Remover"><i class="ti ti-trash"></i></button>
    </div>`;
  });
  document.getElementById('task-list').innerHTML=html;
}

// --- RENDER KANBAN ---
function renderKanban(){
  const cols={todo:[],doing:[],done:[]};
  tasks.forEach(t=>{if(cols[t.kbStatus])cols[t.kbStatus].push(t)});
  const labels={todo:'Aguardando',doing:'Em Análise',done:'Pago'};
  ['todo','doing','done'].forEach(s=>{
    document.getElementById('kb-cnt-'+s).textContent=cols[s].length;
    const el=document.getElementById('kb-'+s);
    if(!cols[s].length){el.innerHTML=`<div class="kb-empty">Nenhuma</div>`;return}
    el.innerHTML=cols[s].map(t=>{
      const urgBg=t.prio==='urgente'?'#FCEBEB':'#FFEED0';
      const urgTxt=t.prio==='urgente'?'#791F1F':'#633806';
      return`<div class="kb-card">
        <div class="kb-card-name">${t.nome}</div>
        <div class="kb-card-meta">
          ${pillHtml(t.setor)}
          <span class="pill" style="background:${urgBg};color:${urgTxt}">${t.prio==='urgente'?'⚠ Urgente':'Normal'}</span>
          ${t.nf?`<span style="font-size:11px;color:#888780">NF: ${t.nf}</span>`:''}
        </div>
        ${t.dataPgto?`<div style="font-size:11px;color:#5F5E5A;margin-bottom:7px"><i class="ti ti-calendar-due" style="font-size:11px"></i> Pgto: ${fmtDateBR(t.dataPgto)}</div>`:''}
        ${t.responsavel?`<div style="font-size:11px;color:#888780;margin-bottom:7px"><i class="ti ti-user" style="font-size:11px"></i> ${t.responsavel}</div>`:''}
        ${t.files&&t.files.length?`<div style="display:flex;flex-wrap:wrap;gap:3px;margin-bottom:7px">${t.files.map((f,fi)=>`<button onclick="downloadFile(${t.id},${fi})" style="font-size:10px;font-family:Poppins,sans-serif;background:#E6F1FB;color:#0C447C;border:1px solid #B8D4EF;border-radius:5px;padding:2px 6px;cursor:pointer;display:inline-flex;align-items:center;gap:2px" title="${f.name}"><i class="ti ti-download" style="font-size:10px"></i>${f.name.length>18?f.name.slice(0,16)+'…':f.name}</button>`).join('')}</div>`:''}
          ${s!=='todo'?`<button class="kb-mv" onclick="mvKb(${t.id},-1)">← voltar</button>`:''}
          ${s!=='done'?`<button class="kb-mv" onclick="mvKb(${t.id},1)">avançar →</button>`:''}
          <button class="kb-mv" onclick="del(${t.id})" style="color:#A32D2D;border-color:#F7C1C1"><i class="ti ti-trash"></i></button>
        </div>
      </div>`;
    }).join('');
  });
}

// --- RENDER DASHBOARD ---
let pieChart=null,diaChart=null,prioChart=null;
function renderDash(){
  const total=tasks.length,done=tasks.filter(t=>t.done).length;
  document.getElementById('d-taxa').textContent=total?Math.round(done/total*100)+'%':'—';
  document.getElementById('d-urg').textContent=tasks.filter(t=>t.prio==='urgente'&&!t.done).length;
  document.getElementById('d-pend').textContent=tasks.filter(t=>!t.done).length;
  document.getElementById('d-setcount').textContent=new Set(tasks.map(t=>t.setor)).size||0;

  // Prio chart
  const nUrgente=tasks.filter(t=>t.prio==='urgente').length;
  const nNormal=tasks.filter(t=>t.prio!=='urgente').length;
  const pUrgente=total?Math.round(nUrgente/total*100):0;
  const pNormal=total?Math.round(nNormal/total*100):0;
  document.getElementById('d-prio-normal-lbl').textContent=`${nNormal} (${pNormal}%)`;
  document.getElementById('d-prio-urgente-lbl').textContent=`${nUrgente} (${pUrgente}%)`;
  document.getElementById('d-prio-normal-bar').style.width=pNormal+'%';
  document.getElementById('d-prio-urgente-bar').style.width=pUrgente+'%';
  if(prioChart){prioChart.destroy();prioChart=null}
  if(total){
    prioChart=new Chart(document.getElementById('chart-prio'),{
      type:'doughnut',
      data:{labels:['Normal','Urgente'],datasets:[{data:[nNormal,nUrgente],backgroundColor:['#3B6D11','#B83232'],borderWidth:2,borderColor:'#fff'}]},
      options:{responsive:true,maintainAspectRatio:false,cutout:'60%',plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`${ctx.label}: ${ctx.parsed} (${total?Math.round(ctx.parsed/total*100):0}%)`}}}}
    });
  }

  const setores={};
  tasks.forEach(t=>{
    if(!setores[t.setor])setores[t.setor]={total:0,done:0};
    setores[t.setor].total++;if(t.done)setores[t.setor].done++;
  });
  const sorted=Object.entries(setores).sort((a,b)=>b[1].total-a[1].total);
  const maxT=Math.max(1,...sorted.map(([,v])=>v.total));
  const noData='<div style="font-size:13px;color:#888780;padding:8px 0">Sem dados ainda</div>';

  document.getElementById('d-setor-bars').innerHTML=sorted.length?sorted.map(([s,v])=>`
    <div class="prog-row">
      <div class="prog-hd"><span>${s}</span><span style="color:#888780">${v.total} solicitaç${v.total>1?'ões':'ão'}</span></div>
      <div class="prog-track"><div class="prog-fill" style="width:${Math.round(v.total/maxT*100)}%;background:${SETOR_COLORS[s]||'#BA7517'}"></div></div>
    </div>`).join(''):noData;

  document.getElementById('d-setor-done').innerHTML=sorted.length?sorted.map(([s,v])=>{
    const p=v.total?Math.round(v.done/v.total*100):0;
    return`<div class="prog-row">
      <div class="prog-hd"><span>${s}</span><span style="color:#888780">${v.done}/${v.total} pagas (${p}%)</span></div>
      <div class="prog-track"><div class="prog-fill" style="width:${p}%;background:${SETOR_COLORS[s]||'#BA7517'}"></div></div>
    </div>`;
  }).join(''):noData;

  if(pieChart){pieChart.destroy();pieChart=null}
  if(sorted.length){
    const pL=sorted.map(([s])=>s);
    const pD=sorted.map(([,v])=>v.total);
    const pC=sorted.map(([s])=>SETOR_COLORS[s]||'#BA7517');
    pieChart=new Chart(document.getElementById('chart-pie'),{
      type:'doughnut',
      data:{labels:pL,datasets:[{data:pD,backgroundColor:pC,borderWidth:2,borderColor:'#FFF8EE'}]},
      options:{responsive:true,maintainAspectRatio:false,cutout:'62%',plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`${ctx.label}: ${ctx.parsed}`}}}}
    });
    const tot=pD.reduce((s,v)=>s+v,0);
    document.getElementById('pie-legend').innerHTML=pL.map((l,i)=>
      `<span style="display:flex;align-items:center;gap:5px;font-size:11px;color:#5F5E5A">
        <span style="width:10px;height:10px;border-radius:2px;background:${pC[i]};flex-shrink:0"></span>
        ${l} — ${pD[i]} (${tot?Math.round(pD[i]/tot*100):0}%)
      </span>`).join('');
  } else {document.getElementById('pie-legend').innerHTML=''}

  if(diaChart){diaChart.destroy();diaChart=null}
  const dm={};
  for(let i=6;i>=0;i--){const d=new Date();d.setDate(d.getDate()-i);dm[d.toISOString().slice(0,10)]=0}
  tasks.forEach(t=>{if(dm[t.data]!==undefined)dm[t.data]++});
  const dL=Object.keys(dm).map(k=>{const[,m,d]=k.split('-');return`${d}/${m}`});
  const dD=Object.values(dm);
  diaChart=new Chart(document.getElementById('chart-dia'),{
    type:'bar',
    data:{labels:dL,datasets:[{data:dD,backgroundColor:dD.map((_,i)=>i===6?'#FEDDB9':'#EFC99A'),borderColor:dD.map((_,i)=>i===6?'#BA7517':'#D3A870'),borderWidth:1,borderRadius:4,borderSkipped:false}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`${ctx.parsed.y} solicitação(ões)`}}},scales:{x:{grid:{display:false},ticks:{font:{size:11,family:'Poppins'}}},y:{grid:{color:'rgba(0,0,0,0.04)'},ticks:{font:{size:11,family:'Poppins'},stepSize:1},beginAtZero:true}}}
  });
}

function render(){
  updateKPIs();
  const v=document.querySelector('.view.on').id.replace('v-','');
  if(v==='agenda')renderAgenda();
  else if(v==='kanban')renderKanban();
  else renderDash();
}

// --- INIT ---
const d=new Date();
const dias=['domingo','segunda','terça','quarta','quinta','sexta','sábado'];
const meses=['janeiro','fevereiro','março','abril','maio','junho','julho','agosto','setembro','outubro','novembro','dezembro'];
document.getElementById('date-display').textContent=`${dias[d.getDay()]}, ${d.getDate()} de ${meses[d.getMonth()]}`;
document.getElementById('f-data').value=todayStr();
document.getElementById('f-nome').addEventListener('keydown',e=>{if(e.key==='Enter')addTask()});
load();
</script>
</body>
</html>
