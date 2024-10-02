<fo:block xsl:use-attribute-sets='Saut_ligne'>  
    <xsl:call-template name="texteEnrichi">  
        <xsl:with-param name="style">  
            <xsl:value-of select="''"/>  
        </xsl:with-param>  
        <xsl:with-param name="texteBrut">  
            <xsl:value-of select="./data/corps/texteLibre"/>  
        </xsl:with-param>  
    </xsl:call-template>  
</fo:block>

<xsl:value-of select="format-number(./data/corps/montantRecours,'# ##0,00','common-currency-fr')"/>