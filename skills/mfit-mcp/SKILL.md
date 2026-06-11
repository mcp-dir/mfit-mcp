---
name: mfit-mcp
description: Skill da REST API do MFIT Personal na MCP.AI: 42 endpoints em /api/mfit. Gestão de alunos, treinos, avaliações físicas, retenção e finanças para personal trainers. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# MFIT Personal — REST API skill

Você tem acesso à **MFIT Personal** REST API na MCP.AI.

> Gestão de alunos, treinos, avaliações físicas, retenção e finanças para personal trainers.

## Base URL

```
https://api.mcp.ai/api/mfit
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/mfit/client/files/delete \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"client_id":"...","file_id":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/mfit/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (42)

#### `mfit_client_files_delete`

Delete a student file (irreversible). _(POST /api/mfit/client/files/delete)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Sim | MFIT student ID |
| `file_id` | string | Sim | File ID |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `file_ids` | string[] | Não | Bulk mode: multiple values for file_id |

#### `mfit_client_files_get`

Read student files/attachments (diet plans, exams, planners, misc). _(POST /api/mfit/client/files/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for list, get) |
| `file_id` | string | Não | File ID (for get) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `file_ids` | string[] | Não | Bulk mode: multiple values for file_id |

#### `mfit_client_files_list`

Read student files/attachments (diet plans, exams, planners, misc). _(POST /api/mfit/client/files/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for list, get) |
| `file_id` | string | Não | File ID (for get) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `file_ids` | string[] | Não | Bulk mode: multiple values for file_id |

#### `mfit_client_files_write`

Update a student file: rename or change sharing settings. _(POST /api/mfit/client/files/write)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `file_id` | string | Sim | File ID |
| `nome` | string | Não | New file name |
| `clients` | number[] | Não | Array of client IDs to share with |
| `groups` | number[] | Não | Array of group IDs to share with |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `file_ids` | string[] | Não | Bulk mode: multiple values for file_id |

#### `mfit_client_get`

Read students in MFIT. _(POST /api/mfit/client/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for get) |
| `status` | string | Não | list: 0/"active" or 1/"inactive" |
| `search` | string | Não | list: filter by name/email/phone |
| `page` | number | Não | list: page number |
| `page_size` | number | Não | list: max 50 |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_client_list`

Read students in MFIT. _(POST /api/mfit/client/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for get) |
| `status` | string | Não | list: 0/"active" or 1/"inactive" |
| `search` | string | Não | list: filter by name/email/phone |
| `page` | number | Não | list: page number |
| `page_size` | number | Não | list: max 50 |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_client_list_groups`

Read students in MFIT. _(POST /api/mfit/client/list/groups)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for get) |
| `status` | string | Não | list: 0/"active" or 1/"inactive" |
| `search` | string | Não | list: filter by name/email/phone |
| `page` | number | Não | list: page number |
| `page_size` | number | Não | list: max 50 |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_client_write_create`

Create / update / deactivate students in MFIT. _(POST /api/mfit/client/write/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for update, deactivate) |
| `name` | string | Não | create/update: first name |
| `lastName` | string | Não | create/update: last name |
| `email` | string | Não | create/update: email |
| `phone` | string | Não | create/update: phone with country code |
| `gender` | string | Não | create/update: m or f |
| `groupId` | string | Não | create/update: Group ID (DYNAMIC — call mfit_client list_groups first) |
| `birthDate` | string | Não | create/update: YYYY-MM-DD |
| `blockOverdue` | boolean | Não | create/update: block if overdue |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_client_write_deactivate`

Create / update / deactivate students in MFIT. _(POST /api/mfit/client/write/deactivate)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for update, deactivate) |
| `name` | string | Não | create/update: first name |
| `lastName` | string | Não | create/update: last name |
| `email` | string | Não | create/update: email |
| `phone` | string | Não | create/update: phone with country code |
| `gender` | string | Não | create/update: m or f |
| `groupId` | string | Não | create/update: Group ID (DYNAMIC — call mfit_client list_groups first) |
| `birthDate` | string | Não | create/update: YYYY-MM-DD |
| `blockOverdue` | boolean | Não | create/update: block if overdue |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_client_write_update`

Create / update / deactivate students in MFIT. _(POST /api/mfit/client/write/update)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (required for update, deactivate) |
| `name` | string | Não | create/update: first name |
| `lastName` | string | Não | create/update: last name |
| `email` | string | Não | create/update: email |
| `phone` | string | Não | create/update: phone with country code |
| `gender` | string | Não | create/update: m or f |
| `groupId` | string | Não | create/update: Group ID (DYNAMIC — call mfit_client list_groups first) |
| `birthDate` | string | Não | create/update: YYYY-MM-DD |
| `blockOverdue` | boolean | Não | create/update: block if overdue |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_get_anamnesis_models`

Get available anamnesis form templates (e.g. PAR-Q) that can be sent to students. _(POST /api/mfit/get/anamnesis/models)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_client_count`

Get a summary count of active and inactive students. _(POST /api/mfit/get/client/count)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_client_evaluations`

Get evaluations for one or many students: heart rate zones, VO2max, and training frequency. _(POST /api/mfit/get/client/evaluations)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID |
| `client_ids` | string[] | Não | Bulk mode: multiple MFIT student IDs |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_client_notes`

Read notes/observations for one or many students (bulk via client_ids). _(POST /api/mfit/get/client/notes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID |
| `client_ids` | string[] | Não | Bulk mode: multiple MFIT student IDs |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_client_notes_write`

Save (overwrite) notes/observations for a student. Replaces any existing notes text. _(POST /api/mfit/get/client/notes/write)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Sim | MFIT student ID |
| `notes` | string | Sim | Notes text content (overwrites existing) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |

#### `mfit_get_client_workouts`

Get all workout routines assigned to one or many students. Supports bulk via client_ids. _(POST /api/mfit/get/client/workouts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID |
| `client_ids` | string[] | Não | Bulk mode: multiple MFIT student IDs |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_exercise_favorites`

Get the trainer's favorite exercises. _(POST /api/mfit/get/exercise/favorites)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_feedbacks`

Get all unread workout feedbacks from students. Each feedback includes: student name, Borg RPE score (1-10 perceived effort), text feedback, workout date/time, duration. Shows which students completed _(POST /api/mfit/get/feedbacks)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_finances`

Get financial overview: transactions in date range, wallet/payment info, seller status. _(POST /api/mfit/get/finances)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `start_date` | string | Sim | Start date YYYY-MM-DD |
| `end_date` | string | Sim | End date YYYY-MM-DD |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_invoices`

Get invoices/billing for one or many students (bulk via client_ids). _(POST /api/mfit/get/invoices)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID |
| `client_ids` | string[] | Não | Bulk mode: multiple MFIT student IDs |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_profile`

Get the trainer's own MFIT profile: name, email, plan, payment country. _(POST /api/mfit/get/profile)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_retention`

Get student retention dashboard: active clients, engagement rate, growth rate, churn rate, NPS. Compare current period vs previous. _(POST /api/mfit/get/retention)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `period` | string | Não | CURRENT_MONTH or date range |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_retention_clients`

List students by retention status: AT_RISK (may churn), ABANDONED (stopped training), ACTIVE, or all. Shows days since last workout, avg weekly workouts, WhatsApp link. Much more useful than listing c _(POST /api/mfit/get/retention/clients)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `status` | string | Não | Filter: AT_RISK, INACTIVE, ACTIVE, or empty for all |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_today_checkins`

Check which students trained today. Scans all active students and returns two lists: who_trained and who_didnt. Single call, no need to check one by one. _(POST /api/mfit/get/today/checkins)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_training_frequency`

Get which days one or many students trained in a date range. Returns true/false per day of week. _(POST /api/mfit/get/training/frequency)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID |
| `client_ids` | string[] | Não | Bulk mode: multiple MFIT student IDs |
| `start_date` | string | Sim | Start date. Accepts YYYY-MM-DD or ISO datetime (e.g. 2026-04-07 or 2026-04-07T00:00:00) |
| `end_date` | string | Sim | End date. Accepts YYYY-MM-DD or ISO datetime (e.g. 2026-04-13 or 2026-04-13T23:59:59) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_training_ranking`

Ranking of students who trained the most in a period (default: current month). Uses bulk frequency checks and returns top performers. _(POST /api/mfit/get/training/ranking)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `month` | string | Não | Optional YYYY-MM. If provided, start_date/end_date are ignored. |
| `start_date` | string | Não | Start date (YYYY-MM-DD or ISO). Used when month is not set. |
| `end_date` | string | Não | End date (YYYY-MM-DD or ISO). Used when month is not set. |
| `status` | string | Não | Client status filter for ranking base list (active, inactive) |
| `limit` | number | Não | How many students to return |
| `include_frequency_payload` | boolean | Não | Include raw training frequency payload for each ranked student |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_user_exercises`

Get custom exercises created by the trainer. _(POST /api/mfit/get/user/exercises)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_get_workout_library`

Browse the trainer's workout library folders and saved routines. Use folder_id=0 for the root. _(POST /api/mfit/get/workout/library)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `folder_id` | number | Não | Folder ID (0 for root) |
| `type` | number | Não |  |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `folder_ids` | number[] | Não | Bulk mode: multiple values for folder_id |

#### `mfit_list_accounts`

List all MFIT accounts linked to this install. _(POST /api/mfit/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_search_exercises`

Search the exercise library by name (Portuguese or English). Returns exercise name, category, muscle group, and video/image URL. _(POST /api/mfit/search/exercises)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `query` | string | Sim | Exercise name (e.g. "supino", "agachamento", "bench press") |
| `page` | number | Não |  |
| `hits_per_page` | number | Não |  |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |

#### `mfit_workout_delete_exercise`

Destructive operations on workout routines, sessions, and exercises. _(POST /api/mfit/workout/delete/exercise)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `routine_id` | string | Não | Routine ID (for delete_routine) |
| `session_id` | string | Não | Session ID (for delete_session, delete_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for delete_exercise) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |

#### `mfit_workout_delete_routine`

Destructive operations on workout routines, sessions, and exercises. _(POST /api/mfit/workout/delete/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `routine_id` | string | Não | Routine ID (for delete_routine) |
| `session_id` | string | Não | Session ID (for delete_session, delete_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for delete_exercise) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |

#### `mfit_workout_delete_session`

Destructive operations on workout routines, sessions, and exercises. _(POST /api/mfit/workout/delete/session)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `routine_id` | string | Não | Routine ID (for delete_routine) |
| `session_id` | string | Não | Session ID (for delete_session, delete_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for delete_exercise) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |

#### `mfit_workout_get_routine`

Read workout routines and sessions in MFIT. _(POST /api/mfit/workout/get/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `routine_id` | string | Não | Routine ID (for get_routine) |
| `session_id` | string | Não | Session ID (for get_session) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |

#### `mfit_workout_get_session`

Read workout routines and sessions in MFIT. _(POST /api/mfit/workout/get/session)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `routine_id` | string | Não | Routine ID (for get_routine) |
| `session_id` | string | Não | Session ID (for get_session) |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |

#### `mfit_workout_write_add_exercise`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/add/exercise)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_archive_routine`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/archive/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_create_routine`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/create/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_create_session`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/create/session)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_unarchive_routine`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/unarchive/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_update_routine`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/update/routine)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

#### `mfit_workout_write_update_serie`

Create / update workout routines, sessions, and exercises in MFIT. _(POST /api/mfit/workout/write/update/serie)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `client_id` | string | Não | MFIT student ID (for create/update_routine, create_session) |
| `routine_id` | string | Não | Routine ID (for update/archive/unarchive_routine, create_session) |
| `session_id` | string | Não | Session ID (for add_exercise) |
| `exercise_id` | string | Não | Exercise ID from search (for add_exercise) |
| `exercise_session_id` | string | Não | Exercise-session ID (for update_serie — from mfit_workout get_session → exerciciosMontados.k{id}[0].idExercSession) |
| `serie_id` | string | Não | update_serie: serie ID from get_session → series[].id |
| `reps` | string | Não | update_serie: e.g. "4x12", "3x15", "3" (just number for time-based) |
| `weight` | string | Não | update_serie: e.g. "30", "50kg", load/weight |
| `rest` | string | Não | update_serie: rest interval in seconds e.g. "60" |
| `name` | string | Não | create/update_routine: routine name / create_session: session name |
| `trainingType` | number | Não | create/update_routine: 1=Dia da Semana, 2=Numérico |
| `goal` | number | Não | create/update_routine: 1=Hipertrofia, 2=Redução gordura, 3=Red.gordura/hipertrofia, 4=Definição, 5=Condicionamento, 6=Qualidade vida |
| `difficulty` | number | Não | create/update_routine: 1=Iniciante, 2=Intermediário, 3=Avançado, 4=Adaptação |
| `instructions` | string | Não | create/update_routine, create_session: general instructions |
| `startDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `endDate` | string | Não | create/update_routine: YYYY-MM-DD |
| `allowPdfDownload` | boolean | Não | create/update_routine: allow PDF download |
| `showTrainingTime` | boolean | Não | create/update_routine: show training timer |
| `day` | number | Não | create_session: 1=Dom, 2=Seg, 3=Ter, 4=Qua, 5=Qui, 6=Sex, 7=Sab |
| `account` | string | Não | Optional account selector when multiple MFIT accounts are linked in this install. Pass the account id, email, or label (full or partial match). Omit if only one account is linked. Use mfit_list_accounts to discover. |
| `client_ids` | string[] | Não | Bulk mode: multiple values for client_id |
| `routine_ids` | string[] | Não | Bulk mode: multiple values for routine_id |
| `session_ids` | string[] | Não | Bulk mode: multiple values for session_id |
| `exercise_ids` | string[] | Não | Bulk mode: multiple values for exercise_id |
| `exercise_session_ids` | string[] | Não | Bulk mode: multiple values for exercise_session_id |
| `serie_ids` | string[] | Não | Bulk mode: multiple values for serie_id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_mfit` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
