# Contributing

Thank you for contributing to **GIB2A**.

## Recommended workflow
1. Fork the repository
2. Create a branch: `feature/<name>` or `fix/<name>`
3. Keep commits small and clear
4. Open a Pull Request including:
   - context (the “why”)
   - screenshots if UI changes
   - radio model + ETHOS version + ProHub version

## ETHOS Lua best practices
- Avoid multiple `lcd.invalidate()` calls in the same wakeup cycle (use a dirty flag)
- Prefer robust sensor identification (IDs/instances) over display names (names can be changed)
- Keep `wakeup()` fast (do the minimum work per loop)
