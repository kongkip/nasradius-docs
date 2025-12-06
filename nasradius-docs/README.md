# NasRadius Documentation

This folder contains the Mintlify documentation for NasRadius.

## Getting Started with Mintlify

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

1. Install Mintlify CLI:
   ```bash
   npm i -g mintlify
   ```

2. Run the development server:
   ```bash
   cd docs
   mintlify dev
   ```

3. Open http://localhost:3000 in your browser

### Deploying

To deploy to Mintlify:

1. Push to your repository
2. Connect to Mintlify dashboard at https://dashboard.mintlify.com
3. Link your repository
4. Deploy automatically on push

## Documentation Structure

```
docs/
├── mint.json                    # Main configuration file
├── introduction.mdx             # Home page
├── getting-started/
│   ├── creating-account.mdx
│   ├── changing-isp-name.mdx
│   └── payment-settings.mdx
├── dashboard/
│   ├── overview.mdx
│   ├── switching-modes.mdx
│   ├── hotspot-dashboard.mdx
│   └── pppoe-dashboard.mdx
├── customers/
│   ├── overview.mdx
│   ├── hotspot-customers.mdx
│   ├── pppoe-customers.mdx
│   └── online-customers.mdx
├── billing/
│   ├── overview.mdx
│   ├── plan-setup.mdx
│   ├── vouchers.mdx
│   └── coupons.mdx
├── payments/
│   ├── overview.mdx
│   ├── associated-payments.mdx
│   ├── unassociated-payments.mdx
│   └── transactions.mdx
├── notifications/
│   ├── overview.mdx
│   ├── sending-notifications.mdx
│   └── notification-history.mdx
├── kopa/
│   ├── overview.mdx
│   ├── analytics.mdx
│   ├── management.mdx
│   ├── plan-management.mdx
│   └── reports.mdx
├── settings/
│   ├── overview.mdx
│   ├── general-settings.mdx
│   ├── sms-settings.mdx
│   ├── balance-reminders.mdx
│   ├── nas-devices.mdx
│   └── payment-settings.mdx
├── mikrotiks/
│   ├── overview.mdx
│   ├── router-list.mdx
│   └── setup-guide.mdx
├── logo/
│   ├── dark.svg
│   └── light.svg
├── favicon.svg
└── images/                      # Add screenshots here
    └── .gitkeep
```

## Adding Images

1. Take screenshots of the NasRadius interface
2. Save them in the `images/` folder
3. Reference them in MDX files:
   ```mdx
   <Frame>
     <img src="/images/your-image.png" alt="Description" />
   </Frame>
   ```

## Customization

### Colors

Edit `mint.json` to change the color scheme:
```json
{
  "colors": {
    "primary": "#00796b",
    "light": "#00bcd4",
    "dark": "#004d40"
  }
}
```

### Navigation

Edit the `navigation` array in `mint.json` to add/remove/reorder pages.

### Adding New Pages

1. Create a new `.mdx` file in the appropriate folder
2. Add frontmatter:
   ```mdx
   ---
   title: Page Title
   description: Page description
   ---
   ```
3. Add the page path to `mint.json` navigation

## Mintlify Components

Common components used in this documentation:

- `<Card>` - Card links
- `<CardGroup>` - Grid of cards
- `<Steps>` - Numbered steps
- `<Accordion>` - Collapsible sections
- `<Tabs>` - Tabbed content
- `<Note>`, `<Warning>`, `<Tip>`, `<Info>` - Callouts
- `<Frame>` - Image frames
- `<ParamField>` - API parameters

## Support

For documentation issues, contact: support@nasradius.com

