# Ceaser-chiper-encoding-and-decoding
def caesar_cipher(message: str, shift: int, mode: str = 'encode') -> str:
    """
    Encodes or decodes a message using the Caesar cipher technique.
    
    Args:
        message: The text to be encoded/decoded
        shift: The number of positions to shift (positive integer)
        mode: 'encode' or 'decode' (default: 'encode')
    
    Returns:
        The encoded/decoded message
    """
    if mode not in ['encode', 'decode']:
        raise ValueError("Mode must be either 'encode' or 'decode'")
    
    if not isinstance(shift, int) or shift < 0:
        raise ValueError("Shift must be a positive integer")
    
    result = []
    shift = shift % 26  # Handle shifts larger than 26
    
    for char in message:
        if char.isupper():
            # Process uppercase letters
            base = ord('A')
            shifted_char = _shift_char(char, base, shift, mode)
            result.append(shifted_char)
        elif char.islower():
            # Process lowercase letters
            base = ord('a')
            shifted_char = _shift_char(char, base, shift, mode)
            result.append(shifted_char)
        else:
            # Leave other characters unchanged
            result.append(char)
    
    return ''.join(result)

def _shift_char(char: str, base: int, shift: int, mode: str) -> str:
    """Helper function to shift a single character"""
    char_code = ord(char) - base
    if mode == 'encode':
        new_code = (char_code + shift) % 26
    else:  # decode
        new_code = (char_code - shift) % 26
    return chr(new_code + base)

# Example usage
if __name__ == "__main__":
    original_message = "Hello, World! 123"
    shift_amount = 5
    
    # Encoding
    encoded = caesar_cipher(original_message, shift_amount, 'encode')
    print(f"Original: {original_message}")
    print(f"Encoded: {encoded}")
    
    # Decoding
    decoded = caesar_cipher(encoded, shift_amount, 'decode')
    print(f"Decoded: {decoded}")
