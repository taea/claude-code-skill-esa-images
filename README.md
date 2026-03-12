# claude-code-skill-esa-images

[Claude Code](https://docs.anthropic.com/en/docs/claude-code) の custom skill（スラッシュコマンド）です。
[esa](https://esa.io/) の記事に添付されている画像を一括ダウンロードします。

## Why?

Claude Code は `img.esa.io` の画像URLを直接閲覧できません。
この skill を使うと、esa 記事内の画像をローカルにダウンロードし、Claude Code の `Read` ツールで閲覧できるようになります。

デザインカンプや参考画像を esa で管理しているチームが、Claude Code でコーディングする際に便利です。

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [esa MCP server](https://github.com/because-and/esa-mcp-server) が設定済みであること

## Install

`SKILL.md` を Claude Code の skills ディレクトリにコピーしてください。

### Personal skill（全プロジェクト共通）

```bash
mkdir -p ~/.claude/skills/esa-images
cp SKILL.md ~/.claude/skills/esa-images/SKILL.md
```

### Project skill（特定プロジェクトのみ）

```bash
mkdir -p .claude/skills/esa-images
cp SKILL.md .claude/skills/esa-images/SKILL.md
```

## Usage

```
/esa-images <team_name> <post_number>
```

### Example

```
/esa-images myteam 826
```

This will:

1. Fetch esa post #826 from the `myteam` team
2. Extract all `img.esa.io` image URLs from the post body
3. Download them to `.design/esa_826/` in your project root
4. Add `.design/` to `.gitignore` if not already present
5. Name files with sequential numbers and descriptive names based on alt text (e.g., `01_top_page.png`)
6. Verify the download by reading a sample image

## Notes

- Images are saved to `.design/esa_{postNumber}/` to keep them separate from source code
- `.design/` is automatically added to `.gitignore`
- If images require authentication and return 403, the skill will notify you
- Retina images (@2x, @4x, etc.) are noted in the output

## License

MIT
