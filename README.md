# Finon iOS design system

The component library for the Finon mobile app (React Native, Expo). These are
the real shipped components. Build screens by composing them; every component
here maps one to one onto code the mobile team ships.

## Foundations

Typography is Inter across the whole system. Four roles, each with size steps:
heading (bold, capitalized: large 28, medium 22, small 18, extraSmall 16), body
(regular: large 18, medium 16, small 14, extraSmall 12), button (bold: 16 / 14 /
12), and label (uppercase 12 bold, or caption 12). Use heading for titles and
numbers that matter, body for supporting copy, label for eyebrows and tags.

Color is a calm blue and neutral system with functional accents:

- Primary blue: a ramp from primary[80] #1E40AF (deepest) through primary[60]
  #1D4ED8 (the default action blue) and primary[30] #3B82F6 up to primary[5]
  #F0F3F8 (the pale field fill) and primary[0] #FFFFFF. Note primary[0] is white,
  not navy.
- Neutral: neutral[100] #272528 for primary text, down through neutral[60]
  #807E83 for secondary text, neutral[20] #DCDCDC for borders, neutral[10]
  #F4F4F2 for surfaces. There is no neutral[0].
- Functional: success green, warning amber, danger red, each with a strong step
  (50/60) and a soft tint (10). Use success for gains, danger for losses and
  destructive actions.
- Accent: turquoise and violet, used sparingly for category tags.

Spacing is a step scale: spacing[1] 4, [2] 8, [3] 12, [4] 16, [5] 24, [6] 32,
[7] 40, [8] 48. Radius: sm 4, md 8 (the default for fields and cards), lg 16
(sheets and large cards), full 9999 (pills).

## Conventions

- Actions are full width pills (radius full). Button supports a filled primary
  default, an outline variant, a color override (use danger red for destructive
  actions), and a disabled state at reduced opacity.
- Inputs sit on the pale primary[5] fill with a leading icon and md radius. The
  Input component is typed by purpose (email, username, password, verify).
- Money and change: gains render in success green, losses in danger red, with a
  directional arrow. Price and percentage always travel together.
- Cards and rows use neutral surfaces and a 1px neutral[20] divider. Asset rows
  lead with the asset name in heading weight and trail with value and a tag.
- Tags are small pills: connection and transaction tags color by category
  (stocks green, crypto violet, savings turquoise, cash blue).
- Screens follow an atomic structure: atoms (Button, Input, Tag, Change),
  molecules (cards, headers, data points, search, pagination), and organisms
  (dashboards, charts, market detail, onboarding steps).

## Notes for composing

- Charts are native modules in the app; in this library they appear as a labeled
  placeholder. Compose the surrounding chrome (totals, time range buttons,
  legends) and treat the chart area as a block.
- Several data components fill from live data at runtime. Their preview cards
  show the real structure with empty or zero values; that is the loading and
  empty state, not a defect.

# FinonDS (finon-app@0.0.0)

This design system is the published finon-app React library, bundled as a single
browser global. All 63 components are the real upstream code.

## Where things are

- `_ds_bundle.js` — the whole-DS bundle at the project root; loads every component to `window.FinonDS`. First line is a `/* @ds-bundle: … */` metadata header.
- `styles.css` — the single stylesheet entry (tokens and fonts; this DS injects component styles at runtime). Link this one file.
- `components/<group>/<Name>/<Name>.prompt.md` (example JSX + variants), `<Name>.d.ts` (types), `<Name>.html` (variant grid).
- `tokens/*.css` — CSS custom properties, names verbatim from upstream.
- `fonts/` — `@font-face` files + `fonts.css` (when the package ships fonts).

For a specific component, `read_file("components/<group>/<Name>/<Name>.prompt.md")`.

## Loading

Add these two lines to your page once (React must be on the page first):

```html
<link rel="stylesheet" href="styles.css">
<script src="_ds_bundle.js"></script>
```

Components are then available at `window.FinonDS.*`. Mount into a dedicated child node (e.g. `<div id="ds-root">`), not the host page's own React root, so the two trees don't collide:

```jsx
const { AddAssetButton } = window.FinonDS;
ReactDOM.createRoot(document.getElementById('ds-root')).render(<AddAssetButton />);
```

Wrap the tree in the provider — most components read theme/i18n from context:

```jsx
<FinonPreviewProvider>{children}</FinonPreviewProvider>
```

## Tokens

0 CSS custom properties from finon-app. Names are
preserved verbatim from upstream. None detected — this DS may compute styles at runtime (CSS-in-JS).



## Components

### atoms
- `AddAssetButton`
- `BackButton`
- `Button`
- `Change`
- `ChartTimeButton`
- `ConnectionTag`
- `Input`
- `LabelChange`
- `Tag`
- `TransactionTag`

### add
- `AddAssetScreen`

### organisms
- `AssetAllocationCard`
- `BottomModal`
- `ChartAsset`
- `ChartInsights`
- `CompanyInformation`
- `ConnectionIssueModal`
- `DashboardList`
- `HorizontalNav`
- `LoadingOverlay`
- `MarketData`
- `MarketsSection`
- `NetChartCard`
- `PlatformSteps`
- `PortfolioChart`
- `ProfileHeader`
- `VerificationCode`

### molecules
- `AssetCardInfo`
- `ChartAssetInfo`
- `ChartCard`
- `ChartCardInfo`
- `ChartInfo`
- `ConnectCard`
- `ConnectionCard`
- `ConnectionSettingCard`
- `DashboardAssetCard`
- `DataPoint`
- `DropdownMenu`
- `FiatCard`
- `Header`
- `HeaderAssetType`
- `IsaAllowanceCard`
- `Pagination`
- `PriceRange`
- `SearchBar`
- `SearchToggle`
- `SelectionGroup`
- `SettingRow`
- `TextContainerButton`
- `TransactionCard`

### connections
- `ConnectionsScreen`

### markets
- `CryptoContent`
- `StockContent`

### general
- `MenuOption`
- `MenuTrigger`
- `StepAuth`
- `StepDone`
- `StepError`
- `StepFileImport`
- `StepKeyCredentials`
- `StepStart`

### portfolio
- `PortfolioScreen`

### user
- `UserScreen`
