---
title: Wdiget Automations
excerpt: >-
  This API will let you create the automations by integrating with the partners
  like Statsperform, OPTA etc, so that you can configure the actions to publish
  the widgets automatically. 
deprecated: false
hidden: false
metadata:
  robots: index
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Automation Partners API</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      font-size: 15px;
      line-height: 1.65;
      color: #1a1a2e;
      background: #f8f9fb;
    }

    /* ── Layout ── */
    .layout {
      display: flex;
      min-height: 100vh;
    }

    nav {
      position: sticky;
      top: 0;
      height: 100vh;
      width: 260px;
      flex-shrink: 0;
      background: #1a1a2e;
      color: #c9d1e0;
      overflow-y: auto;
      padding: 28px 0 40px;
    }

    nav .nav-title {
      font-size: 13px;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: #7b8ab8;
      padding: 0 22px 12px;
    }

    nav a {
      display: block;
      padding: 6px 22px;
      font-size: 13.5px;
      color: #c9d1e0;
      text-decoration: none;
      border-left: 3px solid transparent;
      transition: background 0.15s, border-color 0.15s, color 0.15s;
    }

    nav a:hover {
      background: rgba(255,255,255,0.06);
      color: #fff;
    }

    nav a.active {
      border-left-color: #4f8ef7;
      color: #fff;
      background: rgba(79,142,247,0.12);
    }

    nav .nav-section {
      margin-top: 18px;
    }

    nav .nav-section-label {
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: #4a5578;
      padding: 0 22px 4px;
    }

    main {
      flex: 1;
      min-width: 0;
      padding: 48px 56px 80px;
      max-width: 960px;
    }

    /* ── Typography ── */
    h1 {
      font-size: 2rem;
      font-weight: 700;
      color: #0f172a;
      margin-bottom: 10px;
    }

    h1 + p {
      font-size: 16px;
      color: #475569;
      margin-bottom: 32px;
    }

    h2 {
      font-size: 1.3rem;
      font-weight: 700;
      color: #0f172a;
      margin: 48px 0 16px;
      padding-bottom: 8px;
      border-bottom: 1px solid #e2e8f0;
    }

    h3 {
      font-size: 1.05rem;
      font-weight: 700;
      color: #1e293b;
      margin: 32px 0 12px;
    }

    p { margin-bottom: 12px; }

    a { color: #3b82f6; text-decoration: none; }
    a:hover { text-decoration: underline; }

    hr {
      border: none;
      border-top: 1px solid #e2e8f0;
      margin: 40px 0;
    }

    /* ── Code ── */
    code {
      font-family: "SF Mono", "Fira Code", "Cascadia Code", Consolas, monospace;
      font-size: 0.83em;
      background: #e8edf5;
      color: #c7254e;
      padding: 1px 5px;
      border-radius: 4px;
    }

    pre {
      background: #0f172a;
      color: #e2e8f0;
      border-radius: 10px;
      padding: 20px 22px;
      overflow-x: auto;
      margin: 16px 0 24px;
      font-size: 13px;
      line-height: 1.55;
    }

    pre code {
      background: none;
      color: inherit;
      padding: 0;
      font-size: inherit;
      border-radius: 0;
    }

    /* ── Syntax colours (light JSON highlight) ── */
    .k  { color: #93c5fd; } /* key */
    .s  { color: #86efac; } /* string value */
    .n  { color: #fca5a5; } /* number */
    .b  { color: #fbbf24; } /* boolean / null */
    .p  { color: #94a3b8; } /* punctuation */
    .c  { color: #64748b; font-style: italic; } /* comment */

    /* ── Tables ── */
    .table-wrap { overflow-x: auto; margin: 16px 0 24px; }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13.5px;
    }

    thead tr { background: #f1f5f9; }

    th {
      text-align: left;
      padding: 9px 14px;
      font-weight: 600;
      color: #374151;
      border-bottom: 2px solid #e2e8f0;
      white-space: nowrap;
    }

    td {
      padding: 8px 14px;
      border-bottom: 1px solid #f0f4f8;
      vertical-align: top;
    }

    tr:last-child td { border-bottom: none; }
    tr:hover td { background: #f8fafc; }

    /* ── Badges ── */
    .badge {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 4px;
      font-size: 11.5px;
      font-weight: 700;
      font-family: "SF Mono", monospace;
      letter-spacing: 0.04em;
    }

    .badge-get    { background: #d1fae5; color: #065f46; }
    .badge-post   { background: #dbeafe; color: #1d4ed8; }
    .badge-put    { background: #fef9c3; color: #854d0e; }
    .badge-delete { background: #fee2e2; color: #991b1b; }

    /* ── Endpoint table ── */
    .endpoint-table td:first-child { white-space: nowrap; }

    /* ── Callouts ── */
    .callout {
      border-left: 4px solid;
      padding: 12px 16px;
      border-radius: 0 8px 8px 0;
      margin: 16px 0 24px;
      font-size: 14px;
    }

    .callout-info    { border-color: #3b82f6; background: #eff6ff; color: #1e40af; }
    .callout-warning { border-color: #f59e0b; background: #fffbeb; color: #92400e; }
    .callout-note    { border-color: #8b5cf6; background: #f5f3ff; color: #5b21b6; }

    /* ── Required / optional chips ── */
    .req { color: #ef4444; font-weight: 600; font-size: 12px; }
    .opt { color: #94a3b8; font-size: 12px; }

    /* ── Section anchors ── */
    h2[id], h3[id] { scroll-margin-top: 24px; }

    /* ── Widget kind tabs ── */
    .tabs { display: flex; gap: 6px; margin-bottom: -1px; }
    .tab-btn {
      padding: 6px 16px;
      font-size: 13px;
      font-weight: 600;
      border: 1px solid #e2e8f0;
      border-bottom: none;
      border-radius: 6px 6px 0 0;
      background: #f8f9fb;
      color: #64748b;
      cursor: pointer;
    }
    .tab-btn.active { background: #fff; color: #1a1a2e; border-color: #e2e8f0; }
    .tab-panel { border: 1px solid #e2e8f0; border-radius: 0 8px 8px 8px; padding: 20px; background: #fff; }
    .tab-panel.hidden { display: none; }
  </style>
</head>
<body>

<div class="layout">

  <!-- ── Sidebar ── -->
  <nav id="sidebar">
    <div class="nav-title">Automation Partners</div>
    <a href="#overview">Overview</a>
    <a href="#base-url">Base URL</a>
    <a href="#authentication">Authentication</a>

    <div class="nav-section">
      <div class="nav-section-label">Endpoints</div>
      <a href="#endpoints">All endpoints</a>
      <a href="#query-params">Query parameters</a>
    </div>

    <div class="nav-section">
      <div class="nav-section-label">Concepts</div>
      <a href="#event-category">Event category &amp; subcategory</a>
      <a href="#request-payload">Request payload</a>
      <a href="#automated-actions">automated_actions</a>
      <a href="#widgets-array">widgets array</a>
    </div>

    <div class="nav-section">
      <div class="nav-section-label">Widget payloads</div>
      <a href="#text-poll">text-poll</a>
      <a href="#alert">alert</a>
      <a href="#emoji-slider">emoji-slider</a>
    </div>

    <div class="nav-section">
      <div class="nav-section-label">Reference</div>
      <a href="#template-variables">Template variables</a>
      <a href="#football-actions">Football action types</a>
      <a href="#rugby-actions">Rugby action types</a>
      <a href="#response-format">Response format</a>
      <a href="#examples">Full examples</a>
      <a href="#errors">Error responses</a>
    </div>
  </nav>

  <!-- ── Main content ── -->
  <main>

    <!-- Overview -->
    <h1 id="overview">Automation Partners API</h1>
    <p>
      Live-action automation partners connect a sports event (identified by <code>event_id</code>) to a set
      of automated widget-publishing rules. When a tracked event occurs — a goal, a try, match start — the
      configured widget is automatically published to the linked programme.
    </p>

    <hr />

    <!-- Base URL -->
    <h2 id="base-url">Base URL</h2>
    <pre><code>/{version}/automation-partners/</code></pre>
    <p><code>version</code> is currently <code>v1</code>.</p>

    <hr />

    <!-- Authentication -->
    <h2 id="authentication">Authentication</h2>
    <p>All endpoints require a <strong>Bearer token</strong> from an OAuth2 producer credential.</p>
    <pre><code>Authorization: Bearer &lt;access_token&gt;</code></pre>

    <hr />

    <!-- Endpoints -->
    <h2 id="endpoints">Endpoints</h2>

    <div class="table-wrap">
      <table class="endpoint-table">
        <thead>
          <tr><th>Method</th><th>Path</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><span class="badge badge-get">GET</span></td>
            <td><code>/v1/automation-partners/</code></td>
            <td>List automation partners</td>
          </tr>
          <tr>
            <td><span class="badge badge-post">POST</span></td>
            <td><code>/v1/automation-partners/</code></td>
            <td>Create an automation partner</td>
          </tr>
          <tr>
            <td><span class="badge badge-get">GET</span></td>
            <td><code>/v1/automation-partners/{id}/</code></td>
            <td>Retrieve an automation partner</td>
          </tr>
          <tr>
            <td><span class="badge badge-put">PUT</span></td>
            <td><code>/v1/automation-partners/{id}/</code></td>
            <td>Full update (replaces automated actions)</td>
          </tr>
          <tr>
            <td><span class="badge badge-delete">DELETE</span></td>
            <td><code>/v1/automation-partners/{id}/</code></td>
            <td>Delete an automation partner</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="callout callout-warning">
      <code>PATCH</code> is <strong>not</strong> supported — use <code>PUT</code> for updates.
    </div>

    <hr />

    <!-- Query parameters -->
    <h2 id="query-params">Query Parameters <small style="font-size:0.75rem;font-weight:400;color:#64748b;">GET list</small></h2>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Parameter</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>client_id</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>Filter by application <code>client_id</code></td>
          </tr>
          <tr>
            <td><code>program_id</code></td><td>UUID</td>
            <td><span class="opt">No</span></td>
            <td>Filter by programme UUID</td>
          </tr>
          <tr>
            <td><code>ordering</code></td><td>string</td>
            <td><span class="opt">No</span></td>
            <td>
              One of <code>match_scheduled_at</code>, <code>status</code>,
              <code>automation_status</code>, <code>created_at</code>.
              Prefix with <code>-</code> for descending.
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Event Category -->
    <h2 id="event-category">Event Category, Subcategory and Partner Type</h2>

    <p>
      The <code>event_category</code> + <code>event_subcategory</code> pair identifies the type of event
      and determines the supported <code>partner_type</code> values for that combination.
      The <code>partner_type</code> field is optional — when omitted, the default partner for the
      combination is used. If provided explicitly, <code>partner_type</code> must be one of the supported
      values for that combination.
    </p>

    <p>
      Each category/subcategory combination has a set of supported partners. As new integrations are added,
      a combination may support more than one <code>partner_type</code>.
    </p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th><code>event_category</code></th>
            <th><code>event_subcategory</code></th>
            <th>Supported <code>partner_type</code> values</th>
            <th>Description</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><code>sports</code></td>
            <td><code>football</code></td>
            <td><code>statsperform</code></td>
            <td>Football (association football) match actions</td>
          </tr>
          <tr>
            <td><code>sports</code></td>
            <td><code>rugby</code></td>
            <td><code>opta</code></td>
            <td>Rugby union match actions</td>
          </tr>
        </tbody>
      </table>
    </div>

    <h3>Validation rules</h3>
    <ul style="padding-left: 22px; margin-bottom: 16px; line-height: 2;">
      <li>Both <code>event_category</code> and <code>event_subcategory</code> are <strong>required</strong>.</li>
      <li><code>event_subcategory</code> cannot be provided without <code>event_category</code>.</li>
      <li>The combination must be one of the recognised pairs in the table above.</li>
      <li>If <code>partner_type</code> is provided, it must be one of the supported values for the given combination.</li>
    </ul>

    <hr />

    <!-- Request Payload -->
    <h2 id="request-payload">Request Payload</h2>
    <h3>Top-level fields</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>event_id</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>Partner-specific event/match identifier (e.g. <code>"srm:match:football-test-001"</code>)</td>
          </tr>
          <tr>
            <td><code>event_category</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>Event category — currently always <code>"sports"</code></td>
          </tr>
          <tr>
            <td><code>event_subcategory</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>Event subcategory — see table above</td>
          </tr>
          <tr>
            <td><code>program_id</code></td><td>UUID</td>
            <td><span class="req">Yes</span></td>
            <td>UUID of the programme this partner belongs to</td>
          </tr>
          <tr>
            <td><code>automated_actions</code></td><td>array</td>
            <td><span class="req">Yes</span></td>
            <td>List of action configurations — at least 1 required</td>
          </tr>
          <tr>
            <td><code>partner_type</code></td><td>string</td>
            <td><span class="opt">No</span></td>
            <td>Override the partner type — must be a supported value for the given combination</td>
          </tr>
          <tr>
            <td><code>match_scheduled_at</code></td><td>ISO 8601 datetime</td>
            <td><span class="opt">No</span></td>
            <td>When the match/event is scheduled</td>
          </tr>
          <tr>
            <td><code>widget_timeout</code></td><td>ISO 8601 duration</td>
            <td><span class="opt">No</span></td>
            <td>How long automated widgets stay active (default: <code>"PT15S"</code>)</td>
          </tr>
          <tr>
            <td><code>widget_title</code></td><td>string</td>
            <td><span class="opt">No</span></td>
            <td>Default title for automated widgets</td>
          </tr>
          <tr>
            <td><code>status</code></td><td>boolean</td>
            <td><span class="opt">No</span></td>
            <td>Enable/disable the automation partner (default: <code>false</code>)</td>
          </tr>
          <tr>
            <td><code>sponsor_ids</code></td><td>array of UUIDs</td>
            <td><span class="opt">No</span></td>
            <td>Sponsors to attach to published widgets</td>
          </tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- automated_actions -->
    <h2 id="automated-actions"><code>automated_actions</code> array</h2>

    <p>
      Each element configures one action trigger.
      All widgets within an action must be the <strong>same <code>widget_kind</code></strong>.
    </p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>action_type</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>
              Action type constant — see
              <a href="#football-actions">Football Actions</a> /
              <a href="#rugby-actions">Rugby Actions</a>
            </td>
          </tr>
          <tr>
            <td><code>enabled</code></td><td>boolean</td>
            <td><span class="opt">No</span></td>
            <td>Whether the action is active (default: <code>true</code>)</td>
          </tr>
          <tr>
            <td><code>widgets</code></td><td>array</td>
            <td><span class="req">Yes</span></td>
            <td>Widget variants for this action — minimum 1, maximum 5</td>
          </tr>
          <tr>
            <td><code>publish_delay</code></td><td>ISO 8601 duration</td>
            <td><span class="opt">No</span></td>
            <td>Delay before publishing after the event fires (default: <code>"PT0S"</code>)</td>
          </tr>
          <tr>
            <td><code>max_widgets</code></td><td>integer</td>
            <td><span class="opt">No</span></td>
            <td>Maximum number of widgets published per match for this action</td>
          </tr>
          <tr>
            <td><code>cooldown_minutes</code></td><td>integer</td>
            <td><span class="opt">No</span></td>
            <td>Minimum minutes between consecutive publishes of this action</td>
          </tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- widgets -->
    <h2 id="widgets-array"><code>widgets</code> array</h2>

    <p>
      Each element is a widget variant.
      <strong>A maximum of 5 widgets is allowed per action.</strong>
      One variant is randomly selected at publish time.
    </p>

    <div class="callout callout-info">
      <strong>Create</strong> — omit <code>widget_id</code> to create a new template.<br />
      <strong>Update</strong> — provide <code>widget_id</code> to update an existing template in-place.
      Templates whose <code>widget_id</code> is absent from the <code>PUT</code> body are deleted.
    </div>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>widget_kind</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>One of <code>"text-poll"</code>, <code>"alert"</code>, <code>"emoji-slider"</code></td>
          </tr>
          <tr>
            <td><code>widget_id</code></td><td>UUID</td>
            <td><span class="opt">No</span></td>
            <td>ID of an existing template to update (update only)</td>
          </tr>
          <tr>
            <td><code>payload</code></td><td>object</td>
            <td><span class="req">Yes</span></td>
            <td>Widget-specific content — see below</td>
          </tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Widget Payloads -->
    <h2 id="widget-payloads">Widget Payload Structures</h2>

    <!-- text-poll -->
    <h3 id="text-poll">text-poll</h3>
    <p>Presents a multiple-choice question to viewers.</p>

<pre><code>{
  <span class="k">"widget_kind"</span>: <span class="s">"text-poll"</span>,
  <span class="k">"payload"</span>: {
    <span class="k">"question"</span>: <span class="s">"Who scored the goal?"</span>,
    <span class="k">"options"</span>: [
      { <span class="k">"description"</span>: <span class="s">"Player A"</span> },
      { <span class="k">"description"</span>: <span class="s">"Player B"</span> }
    ],
    <span class="k">"timeout"</span>: <span class="s">"PT30S"</span>,
    <span class="k">"custom_data"</span>: <span class="s">"{\"key\": \"value\"}"</span>,
    <span class="k">"localized_data"</span>: {
      <span class="k">"fr"</span>: {
        <span class="k">"question"</span>: <span class="s">"Qui a marqué le but ?"</span>,
        <span class="k">"options"</span>: [
          { <span class="k">"description"</span>: <span class="s">"Joueur A"</span> },
          { <span class="k">"description"</span>: <span class="s">"Joueur B"</span> }
        ]
      },
      <span class="k">"es"</span>: {
        <span class="k">"question"</span>: <span class="s">"¿Quién marcó el gol?"</span>,
        <span class="k">"options"</span>: [
          { <span class="k">"description"</span>: <span class="s">"Jugador A"</span> },
          { <span class="k">"description"</span>: <span class="s">"Jugador B"</span> }
        ]
      }
    }
  }
}</code></pre>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>question</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>The poll question text. Supports <code>&#123;&#123;variableName&#125;&#125;</code> placeholders — see <a href="#template-variables">Template Variables</a></td>
          </tr>
          <tr>
            <td><code>options</code></td><td>array</td>
            <td><span class="req">Yes</span></td>
            <td>Answer options — each with a <code>"description"</code> string</td>
          </tr>
          <tr>
            <td><code>timeout</code></td><td>ISO 8601 duration</td>
            <td><span class="opt">No</span></td>
            <td>How long the poll accepts votes</td>
          </tr>
          <tr>
            <td><code>custom_data</code></td><td>string (JSON)</td>
            <td><span class="opt">No</span></td>
            <td>Arbitrary JSON string attached to the widget</td>
          </tr>
          <tr>
            <td><code>localized_data</code></td><td>object</td>
            <td><span class="opt">No</span></td>
            <td>BCP-47 locale keys mapping to translated <code>question</code> and <code>options</code></td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- alert -->
    <h3 id="alert">alert</h3>
    <p>Publishes a notification card to viewers.</p>

<pre><code>{
  <span class="k">"widget_kind"</span>: <span class="s">"alert"</span>,
  <span class="k">"payload"</span>: {
    <span class="k">"text"</span>: <span class="s">"⚽ GOAL! {{goalScorer}} scores for {{teamDescription}}!"</span>,
    <span class="k">"title"</span>: <span class="s">"Goal!"</span>,
    <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/goal.png"</span>,
    <span class="k">"link_url"</span>: <span class="s">"https://example.com/match-centre"</span>,
    <span class="k">"link_label"</span>: <span class="s">"View match centre"</span>,
    <span class="k">"timeout"</span>: <span class="s">"PT15S"</span>,
    <span class="k">"custom_data"</span>: <span class="b">null</span>,
    <span class="k">"localized_data"</span>: {
      <span class="k">"fr"</span>: {
        <span class="k">"title"</span>: <span class="s">"But !"</span>,
        <span class="k">"text"</span>: <span class="s">"⚽ BUT ! {{goalScorer}} marque pour {{teamDescription}} !"</span>,
        <span class="k">"link_label"</span>: <span class="s">"Voir le centre de match"</span>
      }
    }
  }
}</code></pre>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>text</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>Alert body text. Supports <code>&#123;&#123;variableName&#125;&#125;</code> placeholders</td>
          </tr>
          <tr>
            <td><code>title</code></td><td>string</td>
            <td><span class="opt">No</span></td>
            <td>Alert heading (max 500 characters)</td>
          </tr>
          <tr>
            <td><code>image_url</code></td><td>URL</td>
            <td><span class="opt">No</span></td>
            <td>Image shown on the alert card</td>
          </tr>
          <tr>
            <td><code>link_url</code></td><td>URL</td>
            <td><span class="opt">No</span></td>
            <td>Call-to-action URL</td>
          </tr>
          <tr>
            <td><code>link_label</code></td><td>string</td>
            <td><span class="opt">No</span></td>
            <td>Label for the call-to-action link</td>
          </tr>
          <tr>
            <td><code>timeout</code></td><td>ISO 8601 duration</td>
            <td><span class="opt">No</span></td>
            <td>How long the alert is visible</td>
          </tr>
          <tr>
            <td><code>custom_data</code></td><td>string (JSON)</td>
            <td><span class="opt">No</span></td>
            <td>Arbitrary JSON string attached to the widget</td>
          </tr>
          <tr>
            <td><code>localized_data</code></td><td>object</td>
            <td><span class="opt">No</span></td>
            <td>BCP-47 locale keys mapping to translated <code>title</code>, <code>text</code>, <code>link_label</code></td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- emoji-slider -->
    <h3 id="emoji-slider">emoji-slider</h3>
    <p>Presents an emoji reaction slider to viewers.</p>

<pre><code>{
  <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
  <span class="k">"payload"</span>: {
    <span class="k">"question"</span>: <span class="s">"Rate that goal! 🔥"</span>,
    <span class="k">"options"</span>: [
      { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/fire.png"</span> },
      { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/meh.png"</span> }
    ],
    <span class="k">"initial_magnitude"</span>: <span class="n">0.5</span>,
    <span class="k">"timeout"</span>: <span class="s">"PT20S"</span>,
    <span class="k">"custom_data"</span>: <span class="b">null</span>,
    <span class="k">"localized_data"</span>: {
      <span class="k">"de"</span>: {
        <span class="k">"question"</span>: <span class="s">"Bewerte dieses Tor! 🔥"</span>
      }
    }
  }
}</code></pre>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Field</th><th>Type</th><th>Required</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>question</code></td><td>string</td>
            <td><span class="req">Yes</span></td>
            <td>The slider question/label. Supports <code>&#123;&#123;variableName&#125;&#125;</code> placeholders</td>
          </tr>
          <tr>
            <td><code>options</code></td><td>array</td>
            <td><span class="req">Yes</span></td>
            <td>Emoji options — each with an <code>"image_url"</code> string</td>
          </tr>
          <tr>
            <td><code>initial_magnitude</code></td><td>decimal (0.0–1.0)</td>
            <td><span class="opt">No</span></td>
            <td>Starting position of the slider (default: <code>0.5</code>)</td>
          </tr>
          <tr>
            <td><code>timeout</code></td><td>ISO 8601 duration</td>
            <td><span class="opt">No</span></td>
            <td>How long the slider accepts responses</td>
          </tr>
          <tr>
            <td><code>custom_data</code></td><td>string (JSON)</td>
            <td><span class="opt">No</span></td>
            <td>Arbitrary JSON string attached to the widget</td>
          </tr>
          <tr>
            <td><code>localized_data</code></td><td>object</td>
            <td><span class="opt">No</span></td>
            <td>BCP-47 locale keys mapping to translated <code>question</code></td>
          </tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Template Variables -->
    <h2 id="template-variables">Template Variables</h2>

    <p>
      Widget text fields support <code>&#123;&#123;variableName&#125;&#125;</code> placeholders that are substituted
      with live event data at publish time. Available variables depend on the action type.
    </p>

    <h3>Football template variables</h3>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Action type</th><th>Available variables</th></tr>
        </thead>
        <tbody>
          <tr><td><code>match_start</code></td><td><code>&#123;&#123;teamDescription&#125;&#125;</code></td></tr>
          <tr><td><code>goal</code></td><td><code>&#123;&#123;goalScorer&#125;&#125;</code></td></tr>
          <tr><td><code>shot</code></td><td><code>&#123;&#123;playerShot&#125;&#125;</code></td></tr>
          <tr><td><code>yellow_card</code></td><td><code>&#123;&#123;cardType&#125;&#125;</code>, <code>&#123;&#123;playerName&#125;&#125;</code>, <code>&#123;&#123;cardReason&#125;&#125;</code></td></tr>
          <tr><td><code>red_card</code></td><td><code>&#123;&#123;cardType&#125;&#125;</code>, <code>&#123;&#123;playerName&#125;&#125;</code>, <code>&#123;&#123;cardReason&#125;&#125;</code></td></tr>
          <tr><td><code>substitution</code></td><td><code>&#123;&#123;playerOffName&#125;&#125;</code>, <code>&#123;&#123;playerOnName&#125;&#125;</code></td></tr>
          <tr><td><code>missed_penalty</code></td><td><code>&#123;&#123;playerMissedPenalty&#125;&#125;</code></td></tr>
          <tr><td><code>var_event</code></td><td><code>&#123;&#123;varType&#125;&#125;</code>, <code>&#123;&#123;varDecision&#125;&#125;</code>, <code>&#123;&#123;varOutcome&#125;&#125;</code>, <code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>foul</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>match_half</code></td><td><em style="color:#94a3b8;">none</em></td></tr>
          <tr><td><code>penalty</code></td><td><em style="color:#94a3b8;">none</em></td></tr>
          <tr><td><code>match_end</code></td><td><em style="color:#94a3b8;">none</em></td></tr>
        </tbody>
      </table>
    </div>

    <h3>Rugby template variables</h3>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Action type</th><th>Available variables</th></tr>
        </thead>
        <tbody>
          <tr><td><code>rugby_match_start</code></td><td><code>&#123;&#123;teamDescription&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_match_end</code></td><td><code>&#123;&#123;teamDescription&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_try</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_conversion</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_penalty_goal</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_drop_goal</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_yellow_card</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_red_card</code></td><td><code>&#123;&#123;playerName&#125;&#125;</code></td></tr>
          <tr><td><code>rugby_match_half</code></td><td><em style="color:#94a3b8;">none</em></td></tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Football Actions -->
    <h2 id="football-actions">Football Action Types</h2>
    <p>Used with <code>event_category: "sports"</code>, <code>event_subcategory: "football"</code>.</p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th><code>action_type</code></th><th>Display name</th><th>Supported widget kinds</th></tr>
        </thead>
        <tbody>
          <tr><td><code>match_start</code></td><td>Match Start</td><td><code>alert</code></td></tr>
          <tr><td><code>match_half</code></td><td>Match Half</td><td><code>text-poll</code></td></tr>
          <tr><td><code>match_end</code></td><td>Match End</td><td><code>text-poll</code></td></tr>
          <tr><td><code>goal</code></td><td>Goal</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>shot</code></td><td>Shot</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>penalty</code></td><td>Penalty</td><td><code>text-poll</code></td></tr>
          <tr><td><code>missed_penalty</code></td><td>Missed Penalty</td><td><code>text-poll</code></td></tr>
          <tr><td><code>yellow_card</code></td><td>Yellow Card</td><td><code>text-poll</code></td></tr>
          <tr><td><code>red_card</code></td><td>Red Card</td><td><code>text-poll</code></td></tr>
          <tr><td><code>substitution</code></td><td>Substitution</td><td><code>text-poll</code></td></tr>
          <tr><td><code>foul</code></td><td>Foul</td><td><code>text-poll</code></td></tr>
          <tr><td><code>var_event</code></td><td>VAR Event</td><td><code>alert</code></td></tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Rugby Actions -->
    <h2 id="rugby-actions">Rugby Action Types</h2>
    <p>Used with <code>event_category: "sports"</code>, <code>event_subcategory: "rugby"</code>.</p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr><th><code>action_type</code></th><th>Display name</th><th>Supported widget kinds</th></tr>
        </thead>
        <tbody>
          <tr><td><code>rugby_match_start</code></td><td>Match Start</td><td><code>alert</code></td></tr>
          <tr><td><code>rugby_match_half</code></td><td>Match Half</td><td><code>text-poll</code></td></tr>
          <tr><td><code>rugby_match_end</code></td><td>Match End</td><td><code>text-poll</code></td></tr>
          <tr><td><code>rugby_try</code></td><td>Try</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>rugby_conversion</code></td><td>Conversion</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>rugby_penalty_goal</code></td><td>Penalty Goal</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>rugby_drop_goal</code></td><td>Drop Goal</td><td><code>emoji-slider</code></td></tr>
          <tr><td><code>rugby_yellow_card</code></td><td>Yellow Card</td><td><code>text-poll</code></td></tr>
          <tr><td><code>rugby_red_card</code></td><td>Red Card</td><td><code>text-poll</code></td></tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Response Format -->
    <h2 id="response-format">Response Format</h2>
    <h3>Success response (single resource)</h3>

<pre><code>{
  <span class="k">"id"</span>: <span class="s">"3fa85f64-5717-4562-b3fc-2c963f66afa6"</span>,
  <span class="k">"event_id"</span>: <span class="s">"srm:match:football-test-001"</span>,
  <span class="k">"event_category"</span>: <span class="s">"sports"</span>,
  <span class="k">"event_subcategory"</span>: <span class="s">"football"</span>,
  <span class="k">"widget_timeout"</span>: <span class="s">"PT15S"</span>,
  <span class="k">"status"</span>: <span class="b">false</span>,
  <span class="k">"widget_title"</span>: <span class="s">"Match Alert"</span>,
  <span class="k">"enabled_by"</span>: {
    <span class="k">"id"</span>: <span class="s">"user-uuid"</span>,
    <span class="k">"name"</span>: <span class="s">"Jane Producer"</span>,
    <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/avatar.png"</span>
  },
  <span class="k">"match_scheduled_at"</span>: <span class="s">"2025-06-15T15:00:00Z"</span>,
  <span class="k">"automation_status"</span>: <span class="s">"scheduled"</span>,
  <span class="k">"automated_actions"</span>: [
    {
      <span class="k">"id"</span>: <span class="s">"action-uuid"</span>,
      <span class="k">"action"</span>: <span class="s">"goal"</span>,
      <span class="k">"status"</span>: <span class="s">"pending"</span>,
      <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
      <span class="k">"publish_delay"</span>: <span class="s">"PT0S"</span>,
      <span class="k">"max_widgets"</span>: <span class="b">null</span>,
      <span class="k">"cooldown_minutes"</span>: <span class="b">null</span>,
      <span class="k">"is_active"</span>: <span class="b">true</span>,
      <span class="k">"created_at"</span>: <span class="s">"2025-06-11T10:00:00Z"</span>,
      <span class="k">"updated_at"</span>: <span class="s">"2025-06-11T10:00:00Z"</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
          <span class="k">"widget_id"</span>: <span class="s">"template-uuid"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"question"</span>: <span class="s">"Rate that goal! 🔥"</span>,
            <span class="k">"options"</span>: [
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/fire.png"</span> }
            ]
          }
        }
      ]
    }
  ]
}</code></pre>

    <h3><code>automation_status</code> values</h3>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Value</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr><td><code>scheduled</code></td><td>Automation is configured and waiting for the event to start</td></tr>
          <tr><td><code>inflight</code></td><td>Automation is actively processing live events</td></tr>
          <tr><td><code>published</code></td><td>Event has ended; automation is complete</td></tr>
        </tbody>
      </table>
    </div>

    <hr />

    <!-- Full Examples -->
    <h2 id="examples">Full Request Examples</h2>

    <h3>Create — Football automation</h3>

<pre><code><span class="c">POST /v1/automation-partners/</span>

{
  <span class="k">"event_id"</span>: <span class="s">"srm:match:20250615-mancity-chelsea"</span>,
  <span class="k">"event_category"</span>: <span class="s">"sports"</span>,
  <span class="k">"event_subcategory"</span>: <span class="s">"football"</span>,
  <span class="k">"program_id"</span>: <span class="s">"a1b2c3d4-e5f6-7890-abcd-ef1234567890"</span>,
  <span class="k">"match_scheduled_at"</span>: <span class="s">"2025-06-15T15:00:00Z"</span>,
  <span class="k">"widget_timeout"</span>: <span class="s">"PT20S"</span>,
  <span class="k">"automated_actions"</span>: [
    {
      <span class="k">"action_type"</span>: <span class="s">"goal"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"question"</span>: <span class="s">"Rate that goal by {{goalScorer}}! 🔥"</span>,
            <span class="k">"options"</span>: [
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/fire.png"</span> },
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/ok.png"</span> }
            ],
            <span class="k">"localized_data"</span>: {
              <span class="k">"fr"</span>: { <span class="k">"question"</span>: <span class="s">"Notez ce but de {{goalScorer}} ! 🔥"</span> },
              <span class="k">"es"</span>: { <span class="k">"question"</span>: <span class="s">"¡Valora el gol de {{goalScorer}}! 🔥"</span> }
            }
          }
        }
      ]
    },
    {
      <span class="k">"action_type"</span>: <span class="s">"match_start"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"alert"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"text"</span>: <span class="s">"🏁 Kick off! {{teamDescription}} are underway!"</span>,
            <span class="k">"title"</span>: <span class="s">"Match Start"</span>,
            <span class="k">"localized_data"</span>: {
              <span class="k">"fr"</span>: {
                <span class="k">"title"</span>: <span class="s">"Début du match"</span>,
                <span class="k">"text"</span>: <span class="s">"🏁 Coup d'envoi ! {{teamDescription}} sont en route !"</span>
              }
            }
          }
        }
      ]
    },
    {
      <span class="k">"action_type"</span>: <span class="s">"yellow_card"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"publish_delay"</span>: <span class="s">"PT3S"</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"text-poll"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"question"</span>: <span class="s">"Was the {{cardType}} for {{playerName}} deserved?"</span>,
            <span class="k">"options"</span>: [
              { <span class="k">"description"</span>: <span class="s">"Yes, fair call"</span> },
              { <span class="k">"description"</span>: <span class="s">"No, too harsh"</span> }
            ],
            <span class="k">"localized_data"</span>: {
              <span class="k">"fr"</span>: {
                <span class="k">"question"</span>: <span class="s">"Le {{cardType}} pour {{playerName}} était-il mérité ?"</span>,
                <span class="k">"options"</span>: [
                  { <span class="k">"description"</span>: <span class="s">"Oui, c'est juste"</span> },
                  { <span class="k">"description"</span>: <span class="s">"Non, trop sévère"</span> }
                ]
              }
            }
          }
        }
      ]
    }
  ]
}</code></pre>

    <h3>Create — Rugby automation</h3>

<pre><code><span class="c">POST /v1/automation-partners/</span>

{
  <span class="k">"event_id"</span>: <span class="s">"opta:match:20250615-saracens-harlequins"</span>,
  <span class="k">"event_category"</span>: <span class="s">"sports"</span>,
  <span class="k">"event_subcategory"</span>: <span class="s">"rugby"</span>,
  <span class="k">"program_id"</span>: <span class="s">"a1b2c3d4-e5f6-7890-abcd-ef1234567890"</span>,
  <span class="k">"match_scheduled_at"</span>: <span class="s">"2025-06-15T14:30:00Z"</span>,
  <span class="k">"automated_actions"</span>: [
    {
      <span class="k">"action_type"</span>: <span class="s">"rugby_try"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"question"</span>: <span class="s">"What did you think of that try by {{playerName}}?"</span>,
            <span class="k">"options"</span>: [
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/amazing.png"</span> },
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/good.png"</span> }
            ],
            <span class="k">"localized_data"</span>: {
              <span class="k">"fr"</span>: { <span class="k">"question"</span>: <span class="s">"Qu'avez-vous pensé de cet essai de {{playerName}} ?"</span> }
            }
          }
        }
      ]
    },
    {
      <span class="k">"action_type"</span>: <span class="s">"rugby_match_start"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"alert"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"text"</span>: <span class="s">"🏉 Kick off! {{teamDescription}} get us underway."</span>,
            <span class="k">"title"</span>: <span class="s">"Match Start"</span>
          }
        }
      ]
    }
  ]
}</code></pre>

    <h3>Update — Full replace (PUT)</h3>

    <div class="callout callout-warning">
      PUT replaces all automated actions. Actions present in the database but absent from the PUT body are
      <strong>deleted</strong>. Widgets not referenced by <code>widget_id</code> are deleted and recreated.
    </div>

<pre><code><span class="c">PUT /v1/automation-partners/3fa85f64-5717-4562-b3fc-2c963f66afa6/</span>

{
  <span class="k">"event_id"</span>: <span class="s">"srm:match:20250615-mancity-chelsea"</span>,
  <span class="k">"event_category"</span>: <span class="s">"sports"</span>,
  <span class="k">"event_subcategory"</span>: <span class="s">"football"</span>,
  <span class="k">"program_id"</span>: <span class="s">"a1b2c3d4-e5f6-7890-abcd-ef1234567890"</span>,
  <span class="k">"match_scheduled_at"</span>: <span class="s">"2025-06-15T15:00:00Z"</span>,
  <span class="k">"automated_actions"</span>: [
    {
      <span class="k">"action_type"</span>: <span class="s">"goal"</span>,
      <span class="k">"enabled"</span>: <span class="b">true</span>,
      <span class="k">"widgets"</span>: [
        {
          <span class="k">"widget_kind"</span>: <span class="s">"emoji-slider"</span>,
          <span class="k">"widget_id"</span>: <span class="s">"template-uuid-to-update"</span>,
          <span class="k">"payload"</span>: {
            <span class="k">"question"</span>: <span class="s">"⚽ GOAL! Rate it!"</span>,
            <span class="k">"options"</span>: [
              { <span class="k">"image_url"</span>: <span class="s">"https://cdn.example.com/fire.png"</span> }
            ]
          }
        }
      ]
    }
  ]
}</code></pre>

    <hr />

    <!-- Errors -->
    <h2 id="errors">Error Responses</h2>

    <p>All errors follow this shape:</p>

<pre><code>{
  <span class="k">"field_name"</span>: [<span class="s">"Error message."</span>]
}</code></pre>

    <p>Or for non-field errors:</p>

<pre><code>{
  <span class="k">"detail"</span>: <span class="s">"Error message."</span>
}</code></pre>

    <h3>Common validation errors</h3>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Error field</th><th>Cause</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><code>event_category</code></td>
            <td>Missing when <code>event_subcategory</code> is provided</td>
          </tr>
          <tr>
            <td><code>event_subcategory</code></td>
            <td>Unknown subcategory for the given <code>event_category</code></td>
          </tr>
          <tr>
            <td><code>partner_type</code></td>
            <td>Provided value is not supported for the given <code>event_category</code> / <code>event_subcategory</code> combination</td>
          </tr>
          <tr>
            <td><code>event_id</code></td>
            <td>Invalid or unrecognised match ID for the partner and programme</td>
          </tr>
          <tr>
            <td><code>program_id</code></td>
            <td>Programme not found under the authenticated application</td>
          </tr>
          <tr>
            <td><code>automated_actions</code></td>
            <td>Missing, empty, or contains an invalid action type or widget kind</td>
          </tr>
          <tr>
            <td><code>error</code></td>
            <td>More than 5 widgets provided for a single action</td>
          </tr>
          <tr>
            <td><code>error</code></td>
            <td>Duplicate automation partner already configured for this programme</td>
          </tr>
        </tbody>
      </table>
    </div>

  </main>
</div>

<script>
  // Highlight active nav link on scroll
  const sections = document.querySelectorAll('[id]');
  const navLinks = document.querySelectorAll('nav a');

  const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        navLinks.forEach(a => a.classList.remove('active'));
        const active = document.querySelector(`nav a[href="#${entry.target.id}"]`);
        if (active) active.classList.add('active');
      }
    });
  }, { rootMargin: '-20% 0px -75% 0px' });

  sections.forEach(s => observer.observe(s));
</script>

</body>
</html>
