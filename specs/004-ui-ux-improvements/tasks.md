# Tasks: UI/UX Improvements

**Feature Branch**: `004-ui-ux-improvements`
**Status**: To Do
**Spec**: [specs/004-ui-ux-improvements/spec.md](spec.md)

## Implementation Strategy
- **Incremental Delivery**: We will implement the backend logic first (DB/API), then built the UI components, and finally integrate them into the pages.
- **Test-Driven**: E2E tests for key user flows (pagination, bulk delete) will be created before UI implementation to guide development.
- **Parallelization**: Frontend components (Pagination, FilterBar, BulkActions) can be built in parallel with backend API updates.

## Dependencies

1. **Phase 1 (Setup)**: Unblocks all phases.
2. **Phase 2 (Foundational)**: Unblocks Phase 3+.
3. **Phase 3 (US1)**: Unblocks advanced UI state management.
4. **Phase 4 (US2)**: Depends on US1 (list view).
5. **Phase 5 (US3)**: Refinement of US1/US2 UI.
6. **Phase 6 (US4)**: Global styling update, can be done anytime after Phase 1 but best last to ensure consistency.

---

## Phase 1: Setup
**Goal**: Initialize project with necessary dependencies and global style configurations.

- [ ] T001 Install @tailwindcss/typography plugin
- [ ] T002 Update src/styles/global.css to include typography plugin and ensure DaisyUI themes are enabled

## Phase 2: Foundational
**Goal**: Establish shared types and database utilities required for advanced features.

- [ ] T003 Update src/lib/types.ts to include FilterOptions interface and extended Evaluation types (with stats)

## Phase 3: Evaluation List Management (US1)
**Goal**: Users can paginate and filter the evaluation list.
**Independent Test**: `tests/e2e/list-management.spec.ts` passes, verifying items limit and filter application.

### Tests
- [ ] T004 [P] [US1] Create E2E test for pagination and filtering in tests/e2e/list-management.spec.ts

### Backend (DB & API)
- [ ] T005 [US1] Update src/lib/db.ts to implement getEvaluations with dynamic filtering (JOIN Result for accuracy)
- [ ] T006 [US1] Update src/pages/api/evaluations/index.ts to handle limit, offset, and filter query parameters

### Frontend Components
- [ ] T007 [P] [US1] Create src/components/Pagination.astro with page size selector
- [ ] T008 [P] [US1] Create src/components/FilterBar.astro with Date and Rubric selectors

### Integration
- [ ] T009 [US1] Update src/pages/index.astro to integrate Pagination and FilterBar with URL state management

## Phase 4: Bulk Data Cleanup (US2)
**Goal**: Users can delete multiple evaluations at once.
**Independent Test**: `tests/e2e/bulk-delete.spec.ts` passes, verifying selected items are removed from DB.

### Tests
- [ ] T010 [P] [US2] Create E2E test for bulk selection and deletion in tests/e2e/bulk-delete.spec.ts

### Backend (DB & API)
- [ ] T011 [US2] Update src/lib/db.ts to implement deleteEvaluations(ids)
- [ ] T012 [US2] Update src/pages/api/evaluations/index.ts to handle DELETE method with JSON body (ids)

### Frontend Components
- [ ] T013 [P] [US2] Create or Refactor src/components/ui/ConfirmationModal.astro for generic usage
- [ ] T014 [P] [US2] Create src/components/BulkActions.astro with select-all logic and delete trigger

### Integration
- [ ] T015 [US2] Update src/pages/index.astro to implement selection state and integrate BulkActions

## Phase 5: Accessibility and Mobile Access (US3)
**Goal**: Interface is responsive and WCAG 2.1 AA compliant.
**Independent Test**: Lighthouse audit passes; mobile view requires no horizontal scroll.

- [ ] T016 [US3] Update src/pages/index.astro table layout to support responsive card view on mobile
- [ ] T017 [US3] Audit and fix ARIA labels and focus management in Pagination, FilterBar, and BulkActions components

## Phase 6: Visual Customization and Consistency (US4)
**Goal**: Consistent typography and functional theme switching.
**Independent Test**: Theme switcher persists preference; typography matches scale.

- [ ] T018 [US4] Update src/components/layout/ThemeController.astro to include Silk, Luxury, Cupcake, Nord themes
- [ ] T019 [US4] Create src/lib/typography.ts to define consistent typography classes/constants
- [ ] T020 [US4] Apply typography scale classes to src/layouts/Layout.astro and main page headers

## Final Phase: Polish
**Goal**: Final verification and performance check.

- [ ] T021 Run full accessibility audit and fix remaining issues
- [ ] T022 Verify performance with large dataset (render time < 200ms)
