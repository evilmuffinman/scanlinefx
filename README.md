-- Set the scanline opacity (0 to 1)
local scanline_opacity = 0.5

function _init()
    original_draw = _draw
    _draw = custom_draw
end

function custom_draw()
    cls()
    original_draw()

    local scanline_color = 0
    for y = 0, 127 do
        if y % 2 == 0 then
            for x = 0, 127 do
                local c = pget(x, y)
                pset(x, y, mid(0, c - flr(scanline_opacity * 15), 15))
            end
        end
    end
end


