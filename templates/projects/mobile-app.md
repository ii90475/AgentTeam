# Mobile App Template

## Description
Native or cross-platform mobile application for iOS and/or Android.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Cross-Platform | React Native, Flutter, Expo |
| iOS Native | Swift, SwiftUI |
| Android Native | Kotlin, Jetpack Compose |
| Backend | Firebase, Supabase, custom API |
| State | Redux, Zustand, MobX, Provider |
| Navigation | React Navigation, Go Router |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Screens, components, services |
| **code-reviewer** | Performance, memory leaks |
| **test-builder** | Unit tests, widget tests |
| **doc-generator** | README, setup guides |
| **changelog-writer** | App store release notes |
| **status-updater** | Sprint progress |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Release planning, feature prioritization |
| **technology-analyst** | Platform decisions, library selection |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── architecture.md
│   ├── project-status.md
│   └── changelog.md
├── src/
│   ├── screens/         # App screens
│   ├── components/      # Reusable UI
│   ├── navigation/      # Navigation config
│   ├── services/        # API, storage
│   ├── store/           # State management
│   ├── hooks/           # Custom hooks
│   └── utils/           # Helpers
├── assets/
│   ├── images/
│   └── fonts/
├── __tests__/
├── ios/                 # iOS native code
├── android/             # Android native code
├── app.json
├── .env.example
└── package.json
```

## Initial Setup Checklist

- [ ] Initialize project (Expo/RN CLI/Flutter)
- [ ] Configure navigation structure
- [ ] Set up state management
- [ ] Configure environment variables
- [ ] Set up API client/services
- [ ] Configure push notifications (if needed)
- [ ] Set up crash reporting (Sentry, Crashlytics)
- [ ] Configure app icons and splash screen
- [ ] Set up CI/CD for app builds
- [ ] Configure app store metadata
