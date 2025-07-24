# Comprehensive Odoo 18 Development Cheatsheet

## Table of Contents
1. [Introduction to Odoo](#introduction-to-odoo)
2. [Development Environment Setup](#development-environment-setup)
3. [Module Structure and Development](#module-structure-and-development)
4. [Models and ORM](#models-and-orm)
5. [Fields](#fields)
6. [Views](#views)
7. [Actions and Menus](#actions-and-menus)
8. [Security](#security)
9. [Inheritance and Extension](#inheritance-and-extension)
10. [OWL Framework](#owl-framework)
11. [JavaScript Framework](#javascript-framework)
12. [QWeb Templates](#qweb-templates)
13. [Reports](#reports)
14. [Wizards](#wizards)
15. [Web Controllers](#web-controllers)
16. [API Integration](#api-integration)
17. [Testing](#testing)
18. [Debugging Techniques](#debugging-techniques)
19. [Performance Optimization](#performance-optimization)
20. [Deployment](#deployment)
21. [Common Patterns and Best Practices](#common-patterns-and-best-practices)

## Introduction to Odoo

### What is Odoo?
- Open-source business management software with modules for ERP, CRM, e-Commerce, etc.
- Built on Python, PostgreSQL, and JavaScript
- Modular architecture allowing for customization and extension
- Available in community (free) and enterprise (paid) editions

### Key Concepts
- **Module**: Self-contained application that adds specific functionality
- **Model**: Represents a business object and defines its structure and behavior
- **View**: Defines how data is displayed to the user
- **Controller**: Handles HTTP requests for web interfaces
- **Business Logic**: Implemented in Python using Odoo's ORM API
- **UI Components**: Built with JavaScript, OWL framework, and QWeb templates

## Development Environment Setup

### System Requirements
- Python 3.10+
- PostgreSQL 12+
- Node.js 16+
- Git

### Installation Methods

#### Docker (Recommended for Development)
```bash
# Pull the official Odoo image
docker pull odoo:18

# Run Odoo with PostgreSQL
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:15
docker run -p 8069:8069 --name odoo --link db:db -t odoo:18
```

#### Source Installation
```bash
# Clone the repository
git clone https://github.com/odoo/odoo.git --depth=1 --branch=18.0 odoo-18
cd odoo-18

# Install dependencies (Debian/Ubuntu)
sudo apt update
sudo apt install git python3-pip build-essential wget python3-dev python3-venv \
    python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev \
    python3-setuptools libpq-dev postgresql postgresql-client libxml2-dev libxslt1-dev \
    libjpeg-dev zlib1g-dev libfreetype6-dev

# Create a virtual environment
python3 -m venv venv
source venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt

# Run Odoo server
./odoo-bin --addons-path=addons -d mydb -i base
```

### Configuration File (odoo.conf)
```ini
[options]
addons_path = /path/to/odoo/addons,/path/to/custom/addons
admin_passwd = admin
db_host = localhost
db_port = 5432
db_user = odoo
db_password = odoo
http_port = 8069
limit_memory_hard = 2684354560
limit_memory_soft = 2147483648
limit_time_cpu = 600
limit_time_real = 1200
list_db = True
log_level = info
```

### Development Tools
- **Visual Studio Code** with Python and Odoo extensions
- **PyCharm** with Odoo plugin
- **Git** for version control
- **pgAdmin** for PostgreSQL management
- **Docker** and **Docker Compose** for containerization

## Module Structure and Development

### Basic Module Structure
```
my_module/
├── __init__.py              # Python package initialization
├── __manifest__.py          # Module descriptor
├── controllers/             # Web controllers
│   ├── __init__.py
│   └── main.py
├── data/                    # Data files (XML)
│   └── initial_data.xml
├── demo/                    # Demo data (XML)
│   └── demo_data.xml
├── models/                  # Business models
│   ├── __init__.py
│   └── models.py
├── security/                # Security files
│   ├── ir.model.access.csv
│   └── security_rules.xml
├── static/                  # Static assets
│   ├── description/         # Module description (for App Store)
│   │   ├── icon.png
│   │   └── index.html
│   ├── src/                 # Source files
│   │   ├── js/
│   │   ├── scss/
│   │   ├── css/
│   │   └── xml/
│   └── lib/                 # Third-party libraries
├── views/                   # View definitions
│   ├── templates.xml
│   └── views.xml
├── wizards/                 # Wizards/pop-up forms
│   ├── __init__.py
│   └── wizard_model.py
└── report/                  # Reporting
    ├── report_template.xml
    └── report.py
```

### Module Manifest File (__manifest__.py)
```python
{
    'name': 'My Module',                  # Module title
    'version': '18.0.1.0.0',              # Version using OCA versioning
    'category': 'Custom',                 # App category
    'summary': 'Short summary',           # Brief description
    'description': """
        Detailed description of the module's functionality.
        Can be multiline.
    """,
    'author': 'Your Name',
    'website': 'https://www.example.com',
    'license': 'LGPL-3',                  # License type
    
    # Dependencies - modules that must be installed
    'depends': ['base', 'mail', 'sale'],
    
    # Data files always installed
    'data': [
        'security/security_groups.xml',
        'security/ir.model.access.csv',
        'data/sequence_data.xml',
        'views/model_views.xml',
        'views/templates.xml',
        'report/report_templates.xml',
        'wizards/wizard_views.xml',
    ],
    
    # Demo data (only loaded in demo mode)
    'demo': [
        'demo/demo_data.xml',
    ],
    
    # QWeb templates for frontend/backend
    'qweb': [
        'static/src/xml/widget_templates.xml',
    ],
    
    # Web assets (Odoo 15+)
    'assets': {
        'web.assets_backend': [
            'my_module/static/src/js/**/*.js',
            'my_module/static/src/scss/**/*.scss',
            'my_module/static/src/xml/**/*.xml',
        ],
        'web.assets_frontend': [
            'my_module/static/src/js/frontend/**/*.js',
            'my_module/static/src/scss/frontend/**/*.scss',
        ],
    },
    
    # Module configuration
    'application': True,        # Is a full application
    'installable': True,        # Can be installed
    'auto_install': False,      # Auto-install if dependencies are met
    'sequence': 10,             # Determines order in module listing
}
```

### Python Files

#### __init__.py (Root)
```python
from . import models
from . import controllers
from . import wizards
from . import report
```

#### models/__init__.py
```python
from . import model_name
from . import another_model
```

#### models/model_name.py
```python
from odoo import models, fields, api, _
from odoo.exceptions import UserError, ValidationError

class ModelName(models.Model):
    _name = 'model.name'
    _description = 'Model Description'
    
    # Model fields and methods defined here
```

## Models and ORM

### Model Definition Types
```python
# Regular model with its own database table
class StandardModel(models.Model):
    _name = 'standard.model'
    _description = 'Standard Model'

# Transient model (temporary data, automatically cleared)
class WizardModel(models.TransientModel):
    _name = 'wizard.model'
    _description = 'Wizard Model'

# Abstract model (inherited by other models, no table)
class AbstractModel(models.AbstractModel):
    _name = 'abstract.model'
    _description = 'Abstract Model'
```

### Model Attributes
```python
class MyModel(models.Model):
    _name = 'my.model'                # Technical name (required)
    _description = 'My Model'         # User-friendly description
    _inherit = 'other.model'          # Inheritance
    _inherits = {'res.partner': 'partner_id'}  # Delegation inheritance
    _order = 'sequence, name'         # Default sort order
    _rec_name = 'display_name'        # Field to use for record name
    _table = 'custom_table_name'      # Custom database table name
    _log_access = True                # Create standard timestamp fields
    _check_company_auto = True        # Auto company domain on relations
    
    # Mail thread integration
    _inherit = ['mail.thread', 'mail.activity.mixin']
    
    # Other common mixins
    _inherit = ['portal.mixin', 'mail.thread', 'mail.activity.mixin', 'image.mixin']
```

### ORM Methods

#### CRUD Operations
```python
# Create record
@api.model
def create(self, vals):
    # Do something before create
    if not vals.get('reference'):
        vals['reference'] = self.env['ir.sequence'].next_by_code('my.model')
    
    record = super().create(vals)
    # Do something after create
    return record

# Update records
def write(self, vals):
    # Do something before update
    result = super().write(vals)
    # Do something after update
    return result

# Delete records
def unlink(self):
    for record in self:
        if record.state == 'done':
            raise UserError(_("Cannot delete records in 'Done' state"))
    
    return super().unlink()

# Copy records (duplicate)
def copy(self, default=None):
    default = dict(default or {})
    default.update({
        'name': _('%s (Copy)') % self.name,
        'reference': False,
    })
    return super().copy(default)
```

#### Search and Read
```python
# Basic search
records = self.env['my.model'].search([('state', '=', 'draft')], limit=10)

# Search with ordering
records = self.env['my.model'].search(
    [('state', '=', 'draft')], 
    order='date desc, name asc', 
    limit=10
)

# Search and count
count = self.env['my.model'].search_count([('state', '=', 'draft')])

# Read specific fields
results = self.env['my.model'].search_read(
    [('state', '=', 'draft')],
    ['name', 'date', 'state'],
    order='date desc',
    limit=10
)

# Name search (used for Many2one fields)
partners = self.env['res.partner'].name_search('john', limit=10)
```

#### Advanced ORM Operations
```python
# Recordset operations
records = self.env['my.model'].browse([1, 2, 3])

# Filtering
draft_records = records.filtered(lambda r: r.state == 'draft')
active_records = records.filtered('active')

# Mapping values
names = records.mapped('name')
partner_cities = records.mapped('partner_id.city')

# Custom mapping function
partner_info = records.mapped(lambda r: (r.partner_id.name, r.partner_id.email))

# Sorting
sorted_records = records.sorted(lambda r: r.date)
sorted_by_name = records.sorted('name')
sorted_by_multiple = records.sorted(lambda r: (r.priority, r.date))

# Grouping
grouped = records.grouped('state')
for state, state_records in grouped:
    print(f"State: {state}, Count: {len(state_records)}")
```

#### Environment and Context
```python
# Access environment components
current_user = self.env.user
current_company = self.env.company
is_superuser = self.env.su

# Change user
records_as_admin = self.with_user(self.env.ref('base.user_admin'))

# Change company
records_in_company = self.with_company(company_id)

# Change context
records_with_ctx = self.with_context(
    force_company=2,
    mail_create_nosubscribe=True,
    default_type='service'
)

# Get context value
lang = self.env.context.get('lang', 'en_US')

# Superuser access
sudo_records = self.sudo()

# Disable tracking
no_track_records = self.with_context(tracking_disable=True)
```

## Fields

### Basic Field Types
```python
from odoo import fields

# Text fields
name = fields.Char('Name', size=64, required=True, translate=True, trim=True)
description = fields.Text('Description', translate=True)
html_content = fields.Html('Content', sanitize=True, strip_style=False)

# Numeric fields
amount = fields.Float('Amount', digits=(16, 2), default=0.0)
quantity = fields.Integer('Quantity', default=1)
price = fields.Monetary('Price', currency_field='currency_id')

# Boolean fields
active = fields.Boolean('Active', default=True)

# Selection fields
state = fields.Selection([
    ('draft', 'Draft'),
    ('confirmed', 'Confirmed'),
    ('done', 'Done'),
    ('cancel', 'Cancelled')
], string='Status', default='draft', required=True, tracking=True)
priority = fields.Selection([
    ('0', 'Low'),
    ('1', 'Normal'),
    ('2', 'High'),
    ('3', 'Very High')
], default='1')

# Date and time fields
date = fields.Date('Date', default=fields.Date.today)
datetime = fields.Datetime('Datetime', default=fields.Datetime.now)

# Binary and image fields
attachment = fields.Binary('Attachment', attachment=True)
image = fields.Image('Image', max_width=1920, max_height=1920, store=True)
```

### Relational Fields
```python
# Many2one (foreign key)
partner_id = fields.Many2one(
    'res.partner',           # Related model
    string='Partner',        # Field label
    required=True,           # Is required
    ondelete='restrict',     # What happens when related record is deleted
    index=True,              # Create database index
    domain=[('is_company', '=', True)],  # Domain filter
    context={'default_is_company': True},  # Default context when creating
    tracking=True            # Track changes
)

# One2many (reverse of Many2one)
line_ids = fields.One2many(
    'my.model.line',         # Related model
    'parent_id',             # Field in related model that references this
    string='Lines',          # Field label
    copy=True,               # Copy when duplicating record
    auto_join=True           # Performance optimization for searches
)

# Many2many
tag_ids = fields.Many2many(
    'my.tag',                # Related model
    'my_model_tag_rel',      # Relation table name
    'model_id',              # Column 1 in relation table
    'tag_id',                # Column 2 in relation table
    string='Tags'            # Field label
)

# Simplified Many2many (let Odoo create relation table)
category_ids = fields.Many2many('product.category', string='Categories')

# Reference field (dynamic relation)
resource_ref = fields.Reference(
    selection=[
        ('res.partner', 'Partner'),
        ('product.product', 'Product'),
    ],
    string='Resource Reference'
)

# Dynamic Reference field selection
def _selection_target_model(self):
    return [(model.model, model.name) for model in self.env['ir.model'].search([])]

resource_ref2 = fields.Reference(
    selection='_selection_target_model',
    string='Resource Reference'
)
```

### Computed and Related Fields
```python
# Computed field (calculated from other fields)
total = fields.Float('Total', compute='_compute_total', store=True, digits=(16, 2))

@api.depends('line_ids.price', 'line_ids.quantity')
def _compute_total(self):
    for record in self:
        record.total = sum(line.price * line.quantity for line in record.line_ids)

# Inverse function (makes computed field editable)
price_unit = fields.Float('Unit Price', compute='_compute_price', inverse='_inverse_price')

@api.depends('total', 'quantity')
def _compute_price(self):
    for record in self:
        record.price_unit = record.total / record.quantity if record.quantity else 0.0

def _inverse_price(self):
    for record in self:
        record.total = record.price_unit * record.quantity

# Related field (access field from related model)
partner_email = fields.Char('Email', related='partner_id.email', readonly=False, store=True)
partner_country_id = fields.Many2one('res.country', related='partner_id.country_id')
```

### Field Attributes
```python
my_field = fields.Char(
    string='Label',              # User-visible label
    required=True,               # Must have a value
    readonly=False,              # Can be edited
    default='Default Value',     # Default value
    index=True,                  # Create database index
    copy=False,                  # Don't copy when duplicating record
    groups='base.group_user',    # Restrict field to specific groups
    states={'draft': [('readonly', False)]},  # State-based attributes
    help='Tooltip help message',  # Help tooltip
    company_dependent=False,     # Multi-company field (ir.property)
    tracking=True,               # Track changes in chatter
    translate=False,             # Enable translations
    store=True,                  # Store computed field in database
    invisible='1',               # For tree/list view
    widget='many2many_tags'      # Specify custom widget
)
```

### Dynamic Defaults and Domains
```python
# Dynamic default using lambda
create_date = fields.Datetime('Created on', default=lambda self: fields.Datetime.now())
company_id = fields.Many2one('res.company', default=lambda self: self.env.company)
user_id = fields.Many2one('res.users', default=lambda self: self.env.user)

# Dynamic domain methods
@api.model
def _get_partner_domain(self):
    return [('customer_rank', '>', 0)]

partner_id = fields.Many2one('res.partner', domain=lambda self: self._get_partner_domain())
```

### Constraints and SQL Constraints
```python
# Python constraint
@api.constrains('date_start', 'date_end')
def _check_dates(self):
    for record in self:
        if record.date_start and record.date_end and record.date_start > record.date_end:
            raise ValidationError(_("Start date must be earlier than end date"))

# SQL Constraints
_sql_constraints = [
    ('name_uniq', 'unique(name, company_id)', 'Name must be unique per company!'),
    ('positive_price', 'CHECK(price >= 0)', 'Price must be positive!'),
]
```

### Onchange Decorators
```python
@api.onchange('partner_id')
def _onchange_partner_id(self):
    if self.partner_id:
        self.email = self.partner_id.email
        self.phone = self.partner_id.phone
        return {
            'domain': {'delivery_address_id': [('parent_id', '=', self.partner_id.id)]},
            'warning': {
                'title': _("Warning"),
                'message': _("This partner has overdue payments!")
            }
        }

@api.onchange('product_id')
def _onchange_product_id(self):
    if self.product_id:
        self.price = self.product_id.list_price
        self.tax_id = self.product_id.taxes_id
```

## Views

### Common View Types

#### Form View
```xml
<record id="view_form" model="ir.ui.view">
    <field name="name">my.model.form</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <form string="My Model">
            <header>
                <!-- Buttons and Status bar -->
                <button name="action_confirm" string="Confirm" type="object" 
                        class="oe_highlight" states="draft"/>
                <button name="action_cancel" string="Cancel" type="object" 
                        states="draft,confirmed"/>
                <button name="%(action_wizard_id)d" string="Launch Wizard" 
                        type="action" context="{'default_model_id': active_id}"/>
                
                <field name="state" widget="statusbar" 
                       statusbar_visible="draft,confirmed,done"/>
            </header>
            
            <sheet>
                <!-- Avatar/Image -->
                <field name="image_1920" widget="image" class="oe_avatar"/>
                
                <!-- Title area -->
                <div class="oe_title">
                    <h1>
                        <field name="name" placeholder="Name"/>
                    </h1>
                </div>
                
                <!-- Button box -->
                <div class="oe_button_box" name="button_box">
                    <button name="action_view_orders" type="object" 
                            class="oe_stat_button" icon="fa-dollar">
                        <field name="order_count" widget="statinfo" string="Orders"/>
                    </button>
                </div>
                
                <!-- Content -->
                <group>
                    <group>
                        <field name="partner_id"/>
                        <field name="email"/>
                        <field name="date"/>
                    </group>
                    <group>
                        <field name="amount"/>
                        <field name="currency_id" options="{'no_create': True}"/>
                        <field name="company_id" groups="base.group_multi_company"/>
                    </group>
                </group>
                
                <notebook>
                    <page string="Lines" name="lines">
                        <field name="line_ids">
                            <tree editable="bottom">
                                <field name="product_id"/>
                                <field name="description"/>
                                <field name="quantity"/>
                                <field name="price_unit"/>
                                <field name="subtotal" sum="Total"/>
                            </tree>
                        </field>
                    </page>
                    <page string="Notes" name="notes">
                        <field name="notes"/>
                    </page>
                </notebook>
            </sheet>
            
            <!-- Chatter (requires mail module) -->
            <div class="oe_chatter">
                <field name="message_follower_ids" widget="mail_followers"/>
                <field name="activity_ids" widget="mail_activity"/>
                <field name="message_ids" widget="mail_thread"/>
            </div>
        </form>
    </field>
</record>
```

#### Tree/List View
```xml
<record id="view_tree" model="ir.ui.view">
    <field name="name">my.model.tree</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <tree string="My Model" decoration-info="state=='draft'" 
              decoration-danger="amount&lt;0" sample="1" multi_edit="1">
            <field name="name"/>
            <field name="partner_id"/>
            <field name="date"/>
            <field name="amount" sum="Total"/>
            <field name="state"/>
            <button name="action_confirm" string="Confirm" type="object" 
                    icon="fa-check" states="draft"/>
        </tree>
    </field>
</record>
```

#### Search View
```xml
<record id="view_search" model="ir.ui.view">
    <field name="name">my.model.search</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <search string="Search My Model">
            <!-- Basic search fields -->
            <field name="name" filter_domain="['|', ('name', 'ilike', self), ('reference', 'ilike', self)]"/>
            <field name="partner_id"/>
            <field name="state"/>
            
            <!-- Predefined filters -->
            <filter string="Draft" name="draft" domain="[('state', '=', 'draft')]"/>
            <filter string="Confirmed" name="confirmed" domain="[('state', '=', 'confirmed')]"/>
            <filter string="Done" name="done" domain="[('state', '=', 'done')]"/>
            
            <!-- Date filters -->
            <filter string="This Month" name="this_month" 
                    domain="[('date', '&gt;=', (context_today() + relativedelta(day=1)).strftime('%Y-%m-%d')),
                             ('date', '&lt;=', (context_today() + relativedelta(months=1, day=1, days=-1)).strftime('%Y-%m-%d'))]"/>
            
            <!-- Group by -->
            <group expand="0" string="Group By">
                <filter string="Partner" name="partner" context="{'group_by': 'partner_id'}"/>
                <filter string="Status" name="status" context="{'group_by': 'state'}"/>
                <filter string="Month" name="month" context="{'group_by': 'date:month'}"/>
            </group>
            
            <!-- Search panel (sidebar) -->
            <searchpanel>
                <field name="company_id" icon="fa-building" enable_counters="1"/>
                <field name="partner_id" select="multi" icon="fa-users" enable_counters="1"/>
            </searchpanel>
        </search>
    </field>
</record>
```

#### Kanban View
```xml
<record id="view_kanban" model="ir.ui.view">
    <field name="name">my.model.kanban</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <kanban default_group_by="state" class="o_kanban_small_column" sample="1">
            <field name="state"/>
            <field name="color"/>
            <field name="partner_id"/>
            <field name="amount"/>
            
            <!-- Configure kanban card appearance -->
            <templates>
                <t t-name="kanban-box">
                    <div t-attf-class="oe_kanban_global_click oe_kanban_card 
                                        #{record.color.raw_value ? 'oe_kanban_color_' + record.color.raw_value : ''}">
                        <div class="oe_kanban_details">
                            <div class="o_kanban_record_top">
                                <div class="o_kanban_record_headings">
                                    <strong class="o_kanban_record_title">
                                        <field name="name"/>
                                    </strong>
                                    <span class="o_kanban_record_subtitle">
                                        <field name="partner_id"/>
                                    </span>
                                </div>
                                <div class="o_dropdown_kanban dropdown">
                                    <a class="dropdown-toggle o-no-caret btn" 
                                       data-toggle="dropdown" href="#" role="button">
                                        <span class="fa fa-ellipsis-v"/>
                                    </a>
                                    <div class="dropdown-menu" role="menu">
                                        <t t-if="widget.editable">
                                            <a type="edit" class="dropdown-item">Edit</a>
                                        </t>
                                        <t t-if="widget.deletable">
                                            <a type="delete" class="dropdown-item">Delete</a>
                                        </t>
                                        <div role="separator" class="dropdown-divider"/>
                                        <div class="o_kanban_colorpicker" role="colorpicker"/>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="o_kanban_record_body">
                                <div><strong>Amount:</strong> <field name="amount" widget="monetary"/></div>
                                <div><field name="date"/></div>
                            </div>
                            
                            <div class="o_kanban_record_bottom">
                                <div class="oe_kanban_bottom_left">
                                    <field name="priority" widget="priority"/>
                                </div>
                                <div class="oe_kanban_bottom_right">
                                    <field name="activity_ids" widget="kanban_activity"/>
                                </div>
                            </div>
                        </div>
                    </div>
                </t>
            </templates>
        </kanban>
    </field>
</record>
```

#### Calendar View
```xml
<record id="view_calendar" model="ir.ui.view">
    <field name="name">my.model.calendar</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <calendar string="My Model Calendar" date_start="date_start" date_stop="date_end" 
                 color="partner_id" mode="month" quick_add="False" event_open_popup="True">
            <field name="name"/>
            <field name="partner_id" filters="1" avatar_field="image_128"/>
        </calendar>
    </field>
</record>
```

#### Pivot View
```xml
<record id="view_pivot" model="ir.ui.view">
    <field name="name">my.model.pivot</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <pivot string="My Model Analysis" sample="1">
            <field name="partner_id" type="row"/>
            <field name="state" type="col"/>
            <field name="amount" type="measure" widget="monetary"/>
            <field name="quantity" type="measure"/>
        </pivot>
    </field>
</record>
```

#### Graph View
```xml
<record id="view_graph" model="ir.ui.view">
    <field name="name">my.model.graph</field>
    <field name="model">my.model</field>
    <field name="arch" type="xml">
        <graph string="My Model Analysis" type="bar" sample="1">
            <field name="partner_id"/>
            <field name="amount" type="measure"/>
        </graph>
    </field>
</record>
```

### Field Widgets
```xml
<!-- Common field widgets -->
<field name="partner_id" widget="many2one_avatar"/>
<field name="tag_ids" widget="many2many_tags" options="{'color_field': 'color'}"/>
<field name="state" widget="badge" decoration-success="state == 'done'" decoration-info="state == 'draft'"/>
<field name="priority" widget="priority"/>
<field name="amount" widget="monetary" options="{'currency_field': 'currency_id'}"/>
<field name="date" widget="daterange" options="{'related_end_date': 'date_end'}"/>
<field name="html_content" widget="html"/>
<field name="image" widget="image" options="{'size': [90, 90]}"/>
<field name="percentage" widget="percentage"/>
<field name="color" widget="color"/>
<field name="activity_ids" widget="mail_activity"/>
<field name="message_ids" widget="mail_thread"/>
<field name="attachment_ids" widget="many2many_binary"/>
<field name="url" widget="url"/>
<field name="signature" widget="signature"/>
<field name="document" widget="pdf_viewer"/>
<field name="barcode" widget="barcode"/>
<field name="progress" widget="progressbar"/>
```

### View Attributes and Options
```xml
<!-- Field attributes -->
<field name="partner_id" 
       required="1" 
       readonly="state != 'draft'" 
       attrs="{'invisible': [('state', '=', 'cancel')], 
               'required': [('type', '=', 'sale')], 
               'readonly': [('state', '!=', 'draft')]}" 
       force_save="1"
       domain="[('is_company', '=', True)]" 
       context="{'default_is_company': True}" 
       options="{'no_create': True, 'no_open': True}" 
       placeholder="Select a partner..." 
       class="oe_inline" 
       groups="base.group_user"/>

<!-- Button attributes -->
<button name="action_confirm" 
        string="Confirm" 
        type="object" 
        class="oe_highlight" 
        confirm="Are you sure you want to confirm this record?" 
        states="draft" 
        groups="base.group_user" 
        icon="fa-check" 
        context="{'key': 'value'}" 
        attrs="{'invisible': [('state', '!=', 'draft')]}"/>

<!-- Button types -->
<button name="action_confirm" type="object"/>  <!-- Call Python method -->
<button name="%(action_wizard_id)d" type="action"/>  <!-- Launch action window -->
<button name="https://www.example.com" type="url"/>  <!-- Open URL -->
```

## Actions and Menus

### Window Action
```xml
<record id="action_my_model" model="ir.actions.act_window">
    <field name="name">My Models</field>
    <field name="res_model">my.model</field>
    <field name="view_mode">tree,form,kanban,calendar,pivot,graph</field>
    <field name="context">{'search_default_draft': 1}</field>
    <field name="domain">[('company_id', '=', current_company_id())]</field>
    <field name="help" type="html">
        <p class="o_view_nocontent_smiling_face">
            Create your first record!
        </p>
    </field>
</record>
```

### Menu Items
```xml
<!-- Top menu item -->
<menuitem id="menu_my_module_root" 
          name="My Module" 
          web_icon="my_module,static/description/icon.png" 
          sequence="10"/>

<!-- Sub menu -->
<menuitem id="menu_my_module_sub" 
          name="My Models" 
          parent="menu_my_module_root" 
          sequence="10"/>

<!-- Action menu item -->
<menuitem id="menu_my_model_list" 
          name="My Models" 
          parent="menu_my_module_sub" 
          action="action_my_model" 
          sequence="10" 
          groups="my_module.group_manager"/>
```

### Server Action
```xml
<record id="action_mark_as_done" model="ir.actions.server">
    <field name="name">Mark as Done</field>
    <field name="model_id" ref="model_my_model"/>
    <field name="binding_model_id" ref="model_my_model"/>
    <field name="binding_view_types">list,form</field>
    <field name="state">code</field>
    <field name="code">
        for record in records:
            if record.state != 'done':
                record.action_done()
    </field>
</record>
```

### URL Action
```xml
<record id="action_open_website" model="ir.actions.act_url">
    <field name="name">Open Website</field>
    <field name="url">https://www.odoo.com</field>
    <field name="target">new</field> <!-- new = new tab/window, self = same window -->
</record>
```

### Client Action
```xml
<record id="action_client_dashboard" model="ir.actions.client">
    <field name="name">Dashboard</field>
    <field name="tag">my_module.dashboard</field>
    <field name="params" eval="{'option': 'value'}"/>
</record>
```

## Security

### Access Control
```xml
<!-- security/ir.model.access.csv -->
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_my_model_user,my.model user,model_my_model,my_module.group_user,1,0,0,0
access_my_model_manager,my.model manager,model_my_model,my_module.group_manager,1,1,1,1
```

### Security Groups
```xml
<!-- security/security_groups.xml -->
<record id="module_category_my_module" model="ir.module.category">
    <field name="name">My Module</field>
    <field name="sequence">10</field>
</record>

<record id="group_user" model="res.groups">
    <field name="name">User</field>
    <field name="category_id" ref="module_category_my_module"/>
    <field name="implied_ids" eval="[(4, ref('base.group_user'))]"/>
</record>

<record id="group_manager" model="res.groups">
    <field name="name">Manager</field>
    <field name="category_id" ref="module_category_my_module"/>
    <field name="implied_ids" eval="[(4, ref('group_user'))]"/>
    <field name="users" eval="[(4, ref('base.user_admin'))]"/>
</record>
```

### Record Rules
```xml
<!-- security/security_rules.xml -->
<record id="rule_my_model_own_records" model="ir.rule">
    <field name="name">My Models: own records only</field>
    <field name="model_id" ref="model_my_model"/>
    <field name="domain_force">[('create_uid', '=', user.id)]</field>
    <field name="groups" eval="[(4, ref('group_user'))]"/>
    <field name="perm_read" eval="True"/>
    <field name="perm_write" eval="True"/>
    <field name="perm_create" eval="True"/>
    <field name="perm_unlink" eval="True"/>
</record>

<record id="rule_my_model_all_records" model="ir.rule">
    <field name="name">My Models: all records</field>
    <field name="model_id" ref="model_my_model"/>
    <field name="domain_force">[(1, '=', 1)]</field>
    <field name="groups" eval="[(4, ref('group_manager'))]"/>
</record>

<!-- Multi-company rule -->
<record id="rule_my_model_company" model="ir.rule">
    <field name="name">My Models: multi-company</field>
    <field name="model_id" ref="model_my_model"/>
    <field name="domain_force">[('company_id', 'in', company_ids)]</field>
    <field name="global" eval="True"/>
</record>
```

## Inheritance and Extension

### Model Inheritance Types

#### Class Inheritance (Extend)
```python
class ExtendedModel(models.Model):
    _inherit = 'existing.model'
    
    # Add new fields
    new_field = fields.Char('New Field')
    
    # Override existing method
    def existing_method(self):
        # Do something before
        res = super(ExtendedModel, self).existing_method()
        # Do something after
        return res
    
    # Add new method
    def new_method(self):
        return True
```

#### Prototype Inheritance (Copy)
```python
class NewModel(models.Model):
    _name = 'new.model'
    _description = 'New Model'
    _inherit = 'existing.model'  # Copy all fields and methods
    
    # Customize as needed
    name = fields.Char('Name', required=True)  # Override field
```

#### Delegation Inheritance (Composition)
```python
class CompositeModel(models.Model):
    _name = 'composite.model'
    _description = 'Composite Model'
    _inherits = {'res.partner': 'partner_id'}  # Delegated inheritance
    
    partner_id = fields.Many2one('res.partner', required=True, ondelete='cascade')
    additional_field = fields.Char('Additional Field')
```

### View Inheritance

#### Extend/Modify View
```xml
<record id="existing_model_form_view_inherit" model="ir.ui.view">
    <field name="name">existing.model.form.inherit</field>
    <field name="model">existing.model</field>
    <field name="inherit_id" ref="original_module.existing_model_form_view"/>
    <field name="arch" type="xml">
        <!-- Add a field after existing field -->
        <field name="existing_field" position="after">
            <field name="new_field"/>
        </field>
        
        <!-- Replace content of a field -->
        <field name="name" position="replace">
            <field name="name" placeholder="Enter name..." attrs="{'required': [('state', '=', 'draft')]}"/>
        </field>
        
        <!-- Add content inside an element -->
        <xpath expr="//group[@name='group_name']" position="inside">
            <field name="new_field"/>
        </xpath>
        
        <!-- Add content before an element -->
        <xpath expr="//field[@name='partner_id']" position="before">
            <field name="priority" widget="priority"/>
        </xpath>
        
        <!-- Add attributes to an element -->
        <xpath expr="//field[@name='date']" position="attributes">
            <attribute name="required">1</attribute>
            <attribute name="attrs">{'readonly': [('state', '!=', 'draft')]}</attribute>
        </xpath>
        
        <!-- Add a new page to notebook -->
        <notebook position="inside">
            <page string="New Page" name="new_page">
                <group>
                    <field name="new_field"/>
                </group>
            </page>
        </notebook>
        
        <!-- Move an existing element -->
        <field name="state" position="move" target="xpath expr='//group[1]'" skip="1"/>
    </field>
</record>
```

#### Inherit Action
```xml
<record id="original_module.action_id" model="ir.actions.act_window">
    <field name="context">{'search_default_filter': 1, 'default_value': True}</field>
    <field name="domain">[('state', '!=', 'cancel')]</field>
    <field name="view_mode">tree,form,kanban</field>
</record>
```

## OWL Framework

### Basic Component Structure
```javascript
/** @odoo-module **/

import { Component, useState, onWillStart } from "@odoo/owl";
import { useService } from "@web/core/utils/hooks";

class MyComponent extends Component {
    setup() {
        // Reactive state
        this.state = useState({
            value: 0,
            items: [],
        });
        
        // Services
        this.orm = useService("orm");
        this.rpc = useService("rpc");
        this.notification = useService("notification");
        
        // Component lifecycle
        onWillStart(async () => {
            const data = await this.loadData();
            this.state.items = data;
        });
    }
    
    async loadData() {
        return this.orm.searchRead("my.model", [["state", "=", "draft"]], ["name", "date", "amount"]);
    }
    
    increment() {
        this.state.value++;
    }
    
    async saveRecord() {
        try {
            await this.orm.write("my.model", [this.props.recordId], {
                name: "New Name",
                value: this.state.value,
            });
            this.notification.add("Record saved successfully", { type: "success" });
        } catch (error) {
            this.notification.add("Failed to save record", { type: "danger" });
        }
    }
}

MyComponent.template = "my_module.MyComponent";
MyComponent.props = {
    recordId: { type: Number, optional: true },
    title: { type: String },
    items: { type: Array, optional: true },
};

export default MyComponent;
```

### OWL Template
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<templates xml:space="preserve">
    <t t-name="my_module.MyComponent" owl="1">
        <div class="my-component">
            <h3 t-esc="props.title" />
            
            <div class="counter">
                <span>Value: <t t-esc="state.value" /></span>
                <button t-on-click="increment" class="btn btn-primary">
                    Increment
                </button>
            </div>
            
            <div class="items" t-if="state.items.length">
                <h4>Items:</h4>
                <ul>
                    <t t-foreach="state.items" t-as="item" t-key="item.id">
                        <li>
                            <span t-esc="item.name" />
                            <span t-if="item.amount" class="amount">
                                (<t t-esc="item.amount" />)
                            </span>
                        </li>
                    </t>
                </ul>
            </div>
            <div t-else="" class="no-items">
                No items found.
            </div>
            
            <button t-on-click="saveRecord" 
                    t-att-disabled="!state.value" 
                    class="btn btn-success">
                Save Record
            </button>
        </div>
    </t>
</templates>
```

### Register Component as Client Action
```javascript
/** @odoo-module **/

import { registry } from "@web/core/registry";
import MyComponent from "./components/my_component";

registry.category("actions").add("my_module.my_action", MyComponent);
```

## JavaScript Framework

### Defining a JavaScript Module
```javascript
/** @odoo-module **/

import { registry } from "@web/core/registry";
import { useService } from "@web/core/utils/hooks";

// Utilities
const rpcErrorHandler = (error) => {
    console.error("RPC Error:", error);
    return Promise.reject(error);
};

// Registering a service
export const myService = {
    dependencies: ["rpc", "notification"],
    
    start(env, { rpc, notification }) {
        return {
            async fetchData(modelName, domain, fields) {
                try {
                    const result = await rpc.query({
                        model: modelName,
                        method: "search_read",
                        args: [domain, fields],
                        kwargs: { limit: 10 },
                    });
                    return result;
                } catch (error) {
                    notification.add("Failed to fetch data", { type: "danger" });
                    return rpcErrorHandler(error);
                }
            },
            
            async createRecord(modelName, data) {
                try {
                    const recordId = await rpc.query({
                        model: modelName,
                        method: "create",
                        args: [data],
                    });
                    notification.add("Record created successfully", { type: "success" });
                    return recordId;
                } catch (error) {
                    notification.add("Failed to create record", { type: "danger" });
                    return rpcErrorHandler(error);
                }
            },
        };
    },
};

registry.category("services").add("myService", myService);
```

### Custom JS Widget (Legacy)
```javascript
/** @odoo-module **/

import Widget from 'web.Widget';
import core from 'web.core';

const QWeb = core.qweb;
const _t = core._t;

var MyWidget = Widget.extend({
    template: 'MyWidgetTemplate',
    events: {
        'click .button_action': '_onButtonClick',
    },
    
    init: function(parent, options) {
        this._super.apply(this, arguments);
        this.options = options || {};
        this.value = this.options.value || 0;
    },
    
    willStart: function() {
        return Promise.all([
            this._super.apply(this, arguments),
            this._loadData(),
        ]);
    },
    
    start: function() {
        this.$counter = this.$('.counter');
        this.$counter.text(this.value);
        return this._super.apply(this, arguments);
    },
    
    _loadData: function() {
        return this._rpc({
            model: 'my.model',
            method: 'search_read',
            args: [[['state', '=', 'draft']], ['name', 'value']],
            kwargs: { limit: 10 },
        }).then(function(records) {
            this.records = records;
        }.bind(this));
    },
    
    _onButtonClick: function(event) {
        event.preventDefault();
        this.value++;
        this.$counter.text(this.value);
        this.trigger_up('value_changed', { value: this.value });
    },
});

return MyWidget;
```

### Field Widget
```javascript
/** @odoo-module **/

import { registry } from "@web/core/registry";
import { standardFieldProps } from "@web/views/fields/standard_field_props";
import { Component, useState } from "@odoo/owl";

class MyFieldWidget extends Component {
    setup() {
        this.state = useState({
            value: this.props.value || 0,
        });
    }
    
    increment() {
        this.state.value++;
        this.props.update(this.state.value);
    }
    
    decrement() {
        if (this.state.value > 0) {
            this.state.value--;
            this.props.update(this.state.value);
        }
    }
}

MyFieldWidget.template = "my_module.MyFieldWidget";
MyFieldWidget.props = {
    ...standardFieldProps,
    value: { type: Number, optional: true },
};

export const myFieldWidget = {
    component: MyFieldWidget,
    supportedTypes: ["integer"],
    extractProps: ({ attrs }) => ({
        min: attrs.min ? Number(attrs.min) : 0,
    }),
};

registry.category("fields").add("my_field_widget", myFieldWidget);
```

## QWeb Templates

### QWeb Directives
```xml
<!-- Basic template with variables and conditionals -->
<t t-name="my_module.Template">
    <!-- Variables -->
    <div t-att-class="'my-class ' + additionalClass">
        <h2 t-esc="title" />  <!-- Escaped output -->
        <div t-raw="rawHtml" />  <!-- Raw HTML output (careful with XSS) -->
        
        <!-- Conditional rendering -->
        <div t-if="condition">
            This is rendered when condition is truthy
        </div>
        <div t-elif="otherCondition">
            This is rendered when condition is falsy but otherCondition is truthy
        </div>
        <div t-else="">
            This is rendered when both conditions are falsy
        </div>
        
        <!-- Loops -->
        <ul>
            <t t-foreach="items" t-as="item" t-key="item.id">
                <li t-att-class="item.done ? 'done' : ''">
                    <span t-esc="item_index + 1"/>. <span t-esc="item.name"/>
                    <t t-if="item_first"> (First item)</t>
                    <t t-if="item_last"> (Last item)</t>
                </li>
            </t>
        </ul>
        
        <!-- Call another template -->
        <t t-call="my_module.SubTemplate">
            <t t-set="subTitle" t-value="'Subtitle'" />
            <t t-set-slot="content">
                <p>This is slot content</p>
            </t>
        </t>
        
        <!-- Evaluating expressions -->
        <div t-esc="value + 5 * 2" />
        <div t-esc="item.price ? '$' + item.price : 'No price'" />
        
        <!-- Setting variables -->
        <t t-set="total" t-value="0" />
        <t t-foreach="items" t-as="item">
            <t t-set="total" t-value="total + item.value" />
        </t>
        <div>Total: <span t-esc="total" /></div>
    </div>
</t>

<!-- Sub-template with slots -->
<t t-name="my_module.SubTemplate">
    <div class="sub-template">
        <h3 t-esc="subTitle" />
        <div class="content">
            <t t-slot="content" />
        </div>
    </div>
</t>
```

### Report Templates
```xml
<template id="report_my_model_document">
    <t t-call="web.html_container">
        <t t-call="web.external_layout">
            <div class="page">
                <h2>
                    <span t-field="doc.name"/>
                </h2>
                
                <div class="row mt32 mb32">
                    <div class="col-6">
                        <strong>Date:</strong>
                        <span t-field="doc.date"/>
                    </div>
                    <div class="col-6">
                        <strong>Reference:</strong>
                        <span t-field="doc.reference"/>
                    </div>
                </div>
                
                <table class="table table-sm">
                    <thead>
                        <tr>
                            <th>Product</th>
                            <th class="text-right">Quantity</th>
                            <th class="text-right">Unit Price</th>
                            <th class="text-right">Subtotal</th>
                        </tr>
                    </thead>
                    <tbody>
                        <t t-foreach="doc.line_ids" t-as="line">
                            <tr>
                                <td><span t-field="line.product_id.name"/></td>
                                <td class="text-right">
                                    <span t-field="line.quantity"/>
                                    <span t-field="line.product_id.uom_id.name" groups="uom.group_uom"/>
                                </td>
                                <td class="text-right">
                                    <span t-field="line.price_unit" t-options='{"widget": "monetary", "display_currency": doc.currency_id}'/>
                                </td>
                                <td class="text-right">
                                    <span t-field="line.subtotal" t-options='{"widget": "monetary", "display_currency": doc.currency_id}'/>
                                </td>
                            </tr>
                        </t>
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="3" class="text-right"><strong>Total</strong></td>
                            <td class="text-right">
                                <span t-field="doc.total" t-options='{"widget": "monetary", "display_currency": doc.currency_id}'/>
                            </td>
                        </tr>
                    </tfoot>
                </table>
                
                <div class="row mt32 mb32">
                    <div class="col-12">
                        <strong>Notes:</strong>
                        <span t-field="doc.notes"/>
                    </div>
                </div>
                
                <div class="oe_structure"/>
            </div>
        </t>
    </t>
</template>
```

## Reports

### PDF Report Definition
```xml
<!-- report/report.xml -->
<record id="action_report_my_model" model="ir.actions.report">
    <field name="name">My Model Report</field>
    <field name="model">my.model</field>
    <field name="report_type">qweb-pdf</field>
    <field name="report_name">my_module.report_my_model</field>
    <field name="report_file">my_module.report_my_model</field>
    <field name="binding_model_id" ref="model_my_model"/>
    <field name="binding_type">report</field>
    <field name="print_report_name">'Report - %s' % (object.name)</field>
</record>

<!-- report/report_templates.xml -->
<template id="report_my_model">
    <t t-call="web.html_container">
        <t t-foreach="docs" t-as="doc">
            <t t-call="my_module.report_my_model_document" t-lang="doc.partner_id.lang"/>
        </t>
    </t>
</template>

<template id="report_my_model_document">
    <!-- Report content here (see QWeb Templates section) -->
</template>
```

### Custom Report Parser
```python
# report/report.py
from odoo import models, api
from datetime import datetime

class MyModelReport(models.AbstractModel):
    _name = 'report.my_module.report_my_model'
    _description = 'My Model Report'
    
    @api.model
    def _get_report_values(self, docids, data=None):
        docs = self.env['my.model'].browse(docids)
        
        # Prepare additional data for the report
        summary = {
            'total_amount': sum(docs.mapped('amount')),
            'count': len(docs),
            'report_date': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
        
        return {
            'doc_ids': docids,
            'doc_model': 'my.model',
            'docs': docs,
            'summary': summary,
            'custom_function': self._custom_function,
        }
    
    def _custom_function(self, value):
        # Helper function available in the report template
        return value * 2
```

### Excel Report
```python
# report/excel_report.py
import base64
import io
from odoo import models, fields, api
from odoo.tools.misc import xlsxwriter

class MyModelExcelReport(models.TransientModel):
    _name = 'my.model.excel.report'
    _description = 'Excel Report for My Model'
    
    date_from = fields.Date('Start Date')
    date_to = fields.Date('End Date')
    
    excel_file = fields.Binary('Excel Report')
    file_name = fields.Char('File Name')
    
    def generate_excel_report(self):
        domain = [('state', '!=', 'cancel')]
        if self.date_from:
            domain.append(('date', '>=', self.date_from))
        if self.date_to:
            domain.append(('date', '<=', self.date_to))
        
        records = self.env['my.model'].search(domain)
        
        # Create Excel file
        output = io.BytesIO()
        workbook = xlsxwriter.Workbook(output)
        worksheet = workbook.add_worksheet('My Model Report')
        
        # Formats
        header_format = workbook.add_format({
            'bold': True, 'bg_color': '#EEEEEE', 'border': 1
        })
        cell_format = workbook.add_format({'border': 1})
        number_format = workbook.add_format({'border': 1, 'num_format': '#,##0.00'})
        
        # Headers
        headers = ['Name', 'Partner', 'Date', 'Amount', 'State']
        for col, header in enumerate(headers):
            worksheet.write(0, col, header, header_format)
        
        # Data
        for row, record in enumerate(records, 1):
            worksheet.write(row, 0, record.name, cell_format)
            worksheet.write(row, 1, record.partner_id.name, cell_format)
            worksheet.write(row, 2, str(record.date), cell_format)
            worksheet.write(row, 3, record.amount, number_format)
            worksheet.write(row, 4, dict(record._fields['state'].selection).get(record.state), cell_format)
        
        # Column width
        worksheet.set_column(0, 0, 30)  # Name
        worksheet.set_column(1, 1, 30)  # Partner
        worksheet.set_column(2, 2, 15)  # Date
        worksheet.set_column(3, 3, 15)  # Amount
        worksheet.set_column(4, 4, 15)  # State
        
        workbook.close()
        
        # Set binary data to the report
        self.excel_file = base64.b64encode(output.getvalue())
        self.file_name = f'My_Model_Report_{fields.Date.today()}.xlsx'
        
        return {
            'type': 'ir.actions.act_url',
            'url': f'web/content?model={self._name}&id={self.id}&field=excel_file&filename={self.file_name}&download=true',
            'target': 'self',
        }
```

## Wizards

### Basic Wizard
```python
# wizards/my_wizard.py
from odoo import models, fields, api, _
from odoo.exceptions import UserError

class MyWizard(models.TransientModel):
    _name = 'my.wizard'
    _description = 'My Wizard'
    
    # Fields
    partner_id = fields.Many2one('res.partner', 'Partner', required=True)
    date = fields.Date('Date', default=fields.Date.today)
    amount = fields.Float('Amount', required=True)
    note = fields.Text('Note')
    
    # Default values from active record
    @api.model
    def default_get(self, fields):
        result = super(MyWizard, self).default_get(fields)
        active_id = self.env.context.get('active_id')
        active_model = self.env.context.
