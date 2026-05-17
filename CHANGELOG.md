# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Multi-language support for `optimization-roadmap.md` (English, Japanese, Korean, Traditional Chinese)
- One-sentence training command feature across all README files
- Simplified training workflow that enables automatic deployment with a single command

### Changed
- Updated Korean README (`README_KO.md`) with native Korean translation for training command
- Restored original Chinese version of `optimization-roadmap.md` after it was incorrectly overwritten
- Improved technical terminology consistency across all language translations

### Fixed
- Chinese character leakage in Korean translation of optimization roadmap
- Terminology alignment: feedforward (피드포워드), integral control (적분 제어), closed-loop (폐쇄 루프), memory (기억/메모리), skills (스킬)

## [0.2.0] - 2026-05-17

### Added
- One-sentence training command feature that enables automatic Agent training with a single prompt
- Simplified training workflow: "按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。"
- Applicable conditions documentation for agents without GitHub access
- Enhanced QUICKSTART.md with updated training instructions

### Changed
- Updated all README files (README.md, README_EN.md, README_ZH_TW.md, README_KO.md) with new training command feature
- Improved user experience with clearer training initiation steps

## [0.1.1] - 2026-05-16

### Added
- `optimization-roadmap.md` - comprehensive optimization roadmap with P0/P1/P2 priority classifications
- Multi-language translations for optimization roadmap (English, Japanese, Korean, Traditional Chinese)
- Technical documentation for 13 optimization items across core infrastructure, system capabilities, and advanced features

### Changed
- Restructured project documentation to include optimization planning
- Enhanced technical governance framework documentation

## [0.1.0] - 2026-05-14

### Added
- `QUICKSTART.md` - quick start guide for immediate deployment
- Simplified deployment instructions with step-by-step commands
- Updated deployment commands in `scripts/deployment-commands.md`
- Streamlined onboarding process for new users

## [0.0.1] - 2026-05-11

### Added
- Initial project release with complete tutorial structure
- Core chapters:
  - Preface (序章)
  - Chapter 1: Background & Core Philosophy (背景与核心理念)
  - Chapter 2: Prerequisites & Preparation (适用条件与准备工作)
  - Chapter 3: Four Control Theory Concepts (四个控制论概念详解)
  - Chapter 4: System Architecture (系统架构详解)
  - Chapter 5: Deployment Guide (实操指南)
  - Chapter 6: Daily Usage & Verification (日常使用与验证方法)
  - Chapter 7: FAQ & Extensions (常见问题与扩展)
  - Epilogue (结尾)
- Multi-language support for README files:
  - `README_EN.md` (English)
  - `README_ZH_TW.md` (Traditional Chinese)
  - `README_KO.md` (Korean)
- Example files:
  - Deep review output example
  - Integral control table example
  - L2/L3 initialization example
- Deployment scripts in `scripts/` directory
- `CONTRIBUTING.md` with contribution guidelines
- `LICENSE` file

[Unreleased]: https://github.com/zeronesun/cybernetic-your-agent/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/zeronesun/cybernetic-your-agent/compare/v0.1.1...v0.2.0
[0.1.1]: https://github.com/zeronesun/cybernetic-your-agent/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/zeronesun/cybernetic-your-agent/compare/v0.0.1...v0.1.0
[0.0.1]: https://github.com/zeronesun/cybernetic-your-agent/releases/tag/v0.0.1